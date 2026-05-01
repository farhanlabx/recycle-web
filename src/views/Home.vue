<template>
  <div class="relative flex flex-col w-full h-screen overflow-hidden" style="background: #050810;">
    <Navbar />

    <!-- Loading overlay -->
    <transition name="fade">
      <div
        v-if="isLoading"
        class="absolute inset-0 z-50 flex flex-col items-center justify-center"
        style="background: #050810;"
      >
        <div class="relative flex items-center justify-center w-32 h-32 mb-8">
          <div class="absolute w-32 h-32 rounded-full border-2 border-green-500/20 animate-ping" />
          <div class="absolute w-24 h-24 rounded-full border-2 border-green-400/30" style="animation: spin 3s linear infinite;" />
          <div class="absolute w-16 h-16 rounded-full border-t-2 border-green-400" style="animation: spin 1s linear infinite;" />
          <span class="text-green-400 text-2xl">♻️</span>
        </div>
        <p class="text-green-400 font-mono font-bold tracking-widest text-sm uppercase mb-2">Memuat Model 3D</p>
        <div class="w-48 h-1 bg-gray-800 rounded-full overflow-hidden">
          <div
            class="h-full bg-gradient-to-r from-green-500 to-emerald-400 rounded-full transition-all duration-300"
            :style="{ width: loadPercent + '%' }"
          />
        </div>
        <p class="text-gray-600 font-mono text-xs mt-2">{{ loadPercent }}%</p>
      </div>
    </transition>

    <!-- Error state -->
    <div
      v-if="loadError"
      class="absolute inset-0 z-50 flex items-center justify-center"
      style="background: #050810;"
    >
      <div class="text-center p-8 border border-red-900/50 rounded-2xl bg-red-950/20 max-w-md">
        <p class="text-red-400 text-4xl mb-4">⚠️</p>
        <p class="text-red-400 font-mono font-bold text-lg mb-2">Gagal Memuat Model</p>
        <p class="text-gray-500 font-mono text-sm mb-4">{{ loadError }}</p>
        <p class="text-gray-700 font-mono text-xs">Pastikan file ada di: <span class="text-green-600">public/3dTrash.glb</span></p>
      </div>
    </div>

    <!-- Hero text overlay -->
    <div v-if="!isLoading && !loadError" class="absolute inset-0 z-10 pointer-events-none flex flex-col justify-end p-12">
      <div ref="heroBottom" class="opacity-0 flex items-end justify-between w-full">

        <!-- LEFT: eyebrow + headline -->
        <div class="max-w-lg">
          <p class="text-green-500 font-mono text-xs tracking-[0.28em] uppercase mb-4 flex items-center gap-2">
            <span class="w-1.5 h-1.5 rounded-full bg-green-500 inline-block animate-pulse"></span>
            Recycle Initiative
          </p>
          <h1
            class="text-white font-black leading-[1.04] tracking-tight"
            style="font-size: clamp(34px, 3.8vw, 56px); letter-spacing: -2px;"
          >
            Recycling Shouldn't<br/>
            Be <span class="text-transparent" style="-webkit-text-stroke: 1.5px #22c55e;">Hard To Find.</span>
          </h1>
        </div>

        <!-- RIGHT: sub-headline + buttons -->
        <div class="max-w-xs flex flex-col items-end gap-5">
          <p class="text-gray-500 font-mono text-sm text-right leading-relaxed">
            Discover nearby recycling centers, learn what you can recycle, and make sustainable living part of everyday life.
          </p>
          <div class="flex flex-col gap-2.5 items-end pointer-events-auto">
            <button class="bg-green-500 hover:bg-green-400 text-gray-950 font-bold text-sm px-7 py-3 rounded-xl transition-colors whitespace-nowrap">
              📍 Find Nearby Locations
            </button>
            <button class="border border-white/10 hover:border-white/30 text-white/40 hover:text-white/70 font-medium text-sm px-6 py-2.5 rounded-xl transition-colors whitespace-nowrap">
              Explore Materials →
            </button>
          </div>
        </div>

      </div>
    </div>

    <!-- Gradient overlays -->
    <div class="absolute inset-0 z-[5] pointer-events-none">
      <div class="absolute inset-x-0 bottom-0 h-40" style="background: linear-gradient(to top, #050810, transparent);" />
      <div class="absolute inset-y-0 left-0 w-32" style="background: linear-gradient(to right, #050810aa, transparent);" />
      <div class="absolute inset-y-0 right-0 w-32" style="background: linear-gradient(to left, #050810aa, transparent);" />
    </div>

    <!-- Drag hint -->
    <div v-if="!isLoading && !loadError" class="absolute bottom-14 left-1/2 -translate-x-1/2 z-10 pointer-events-none">
      <p class="text-gray-700 font-mono text-xs tracking-widest">DRAG TO ROTATE · SCROLL TO ZOOM</p>
    </div>

    <!-- Three.js canvas -->
    <div ref="mountRef" class="absolute inset-0 z-0" />
  </div>
</template>

<script setup>
// ── 1. nextTick added here ──────────────────────────────────────────────────
import { ref, onMounted, onBeforeUnmount, nextTick } from 'vue'
import * as THREE from 'three'
import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader.js'
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js'
import gsap from 'gsap'
import Navbar from '../components/navbar.vue'

const mountRef    = ref(null)
const heroBottom  = ref(null)
const isLoading   = ref(true)
const loadError   = ref(null)
const loadPercent = ref(0)

let renderer, scene, camera, controls, animationId, model
let floatTween = null

onMounted(() => {
  initScene()
  loadModel()
  animate()
  window.addEventListener('resize', onResize)
})

onBeforeUnmount(() => {
  cancelAnimationFrame(animationId)
  window.removeEventListener('resize', onResize)
  floatTween?.kill()
  gsap.killTweensOf(model?.position)
  gsap.killTweensOf(model?.rotation)
  controls?.dispose()
  renderer?.dispose()
})

function initScene() {
  const container = mountRef.value
  const w = container.clientWidth
  const h = container.clientHeight

  scene = new THREE.Scene()
  scene.background = new THREE.Color(0x050810)
  scene.fog = new THREE.FogExp2(0x050810, 0.035)

  camera = new THREE.PerspectiveCamera(45, w / h, 0.1, 100)
  camera.position.set(0, 1.5, 6)

  renderer = new THREE.WebGLRenderer({ antialias: true, alpha: false })
  renderer.setSize(w, h)
  renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2))
  renderer.shadowMap.enabled = true
  renderer.shadowMap.type = THREE.PCFShadowMap
  renderer.outputColorSpace = THREE.SRGBColorSpace
  renderer.toneMapping = THREE.ACESFilmicToneMapping
  renderer.toneMappingExposure = 1.1
  container.appendChild(renderer.domElement)

  controls = new OrbitControls(camera, renderer.domElement)
  controls.enableDamping = true
  controls.dampingFactor = 0.06
  controls.autoRotate = true
  controls.autoRotateSpeed = 0.8
  controls.minDistance = 2
  controls.maxDistance = 12
  controls.maxPolarAngle = Math.PI / 1.8
  controls.target.set(0, 0, 0)

  scene.add(new THREE.AmbientLight(0xffffff, 0.6))

  const dirLight = new THREE.DirectionalLight(0xffffff, 2.5)
  dirLight.position.set(5, 10, 5)
  dirLight.castShadow = true
  dirLight.shadow.mapSize.set(1024, 1024)
  dirLight.shadow.camera.near = 0.5
  dirLight.shadow.camera.far = 30
  dirLight.shadow.camera.left = -5
  dirLight.shadow.camera.right = 5
  dirLight.shadow.camera.top = 5
  dirLight.shadow.camera.bottom = -5
  scene.add(dirLight)

  const fillLight = new THREE.PointLight(0x22ff88, 2, 15)
  fillLight.position.set(-4, 3, -3)
  scene.add(fillLight)

  const rimLight = new THREE.PointLight(0x4499ff, 1.5, 12)
  rimLight.position.set(4, 5, -4)
  scene.add(rimLight)

  const bounceLight = new THREE.PointLight(0xffaa44, 0.5, 8)
  bounceLight.position.set(0, -2, 2)
  scene.add(bounceLight)

  const ground = new THREE.Mesh(
    new THREE.PlaneGeometry(20, 20),
    new THREE.ShadowMaterial({ opacity: 0.35, transparent: true })
  )
  ground.rotation.x = -Math.PI / 2
  ground.position.y = -1.6
  ground.receiveShadow = true
  scene.add(ground)
}

function loadModel() {
  const loader = new GLTFLoader()

  // ── 2. async added to callback so await nextTick() works inside ────────────
  loader.load(
    '/3dTrash.glb',
    async (gltf) => {
      model = gltf.scene

      const box = new THREE.Box3().setFromObject(model)
      const size = box.getSize(new THREE.Vector3())
      const maxDim = Math.max(size.x, size.y, size.z)
      const scale = 2.5 / maxDim
      model.scale.setScalar(scale)

      const box2 = new THREE.Box3().setFromObject(model)
      const center2 = box2.getCenter(new THREE.Vector3())

      model.position.x = -center2.x
      model.position.z = -center2.z
      model.position.y = -box2.min.y

      model.traverse((child) => {
        if (child.isMesh) {
          child.castShadow = true
          child.receiveShadow = true
        }
      })

      const restY = model.position.y
      model.position.y = restY + 5
      model.rotation.y = Math.PI
      scene.add(model)

      // ── 3. set loading false, then wait for Vue to render the v-if block ───
      isLoading.value = false
      await nextTick()  // heroBottom.value is now guaranteed to exist in the DOM

      gsap.to(model.position, {
        y: restY,
        duration: 1.6,
        ease: 'power4.out',
        onComplete: startFloat
      })
      gsap.to(model.rotation, {
        y: 0,
        duration: 2,
        ease: 'expo.out'
      })

      gsap.to(heroBottom.value, {
        opacity: 1,
        y: 0,
        duration: 1,
        delay: 0.8,
        ease: 'power3.out'
      })

      function startFloat() {
        floatTween = gsap.to(model.position, {
          y: restY + 0.15,
          duration: 2.2,
          repeat: -1,
          yoyo: true,
          ease: 'sine.inOut'
        })
      }
    },
    (progress) => {
      if (progress.total > 0) {
        loadPercent.value = Math.round((progress.loaded / progress.total) * 100)
      }
    },
    (error) => {
      console.error('GLB Error:', error)
      loadError.value = error.message || 'Unknown error'
      isLoading.value = false
    }
  )
}

function animate() {
  animationId = requestAnimationFrame(animate)
  controls?.update()
  renderer?.render(scene, camera)
}

function onResize() {
  const container = mountRef.value
  if (!container) return
  const w = container.clientWidth
  const h = container.clientHeight
  camera.aspect = w / h
  camera.updateProjectionMatrix()
  renderer.setSize(w, h)
}
</script>

<style scoped>
@keyframes spin {
  from { transform: rotate(0deg); }
  to   { transform: rotate(360deg); }
}
.fade-enter-active,
.fade-leave-active { transition: opacity 0.6s ease; }
.fade-enter-from,
.fade-leave-to { opacity: 0; }
</style>