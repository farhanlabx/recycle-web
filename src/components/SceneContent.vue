<!-- src/components/SceneContent.vue -->
<template>
  <TresGroup :position="[0, -1, 0]">
    <Model3D />
    <OrbitControls auto-rotate :auto-rotate-speed="0.5" enable-damping />
  </TresGroup>
</template>

<script setup>
import { OrbitControls } from '@tresjs/cientos'
import Model3D from './Model3D.vue'
</script>