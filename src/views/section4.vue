<script setup>
import { onMounted } from 'vue'
import L from 'leaflet'
import 'leaflet/dist/leaflet.css'

const defaultLat = -8.7
const defaultLng = 115.2

const pinIcon = L.divIcon({
  className: '',
  html: '<div style="background:#3a7d5c; width:14px; height:14px; border-radius:50%; border:3px solid white; box-shadow:0 2px 6px rgba(0,0,0,0.3);"></div>',
  iconSize: [14, 14],
  iconAnchor: [7, 7]
})

function tambahinMarker(map, lat, lng, nama, detail) {
  L.marker([lat, lng], { icon: pinIcon })
    .addTo(map)
    .bindPopup(`<b>${nama}</b><br>${detail}`)
}

function loadMap(map, lat, lng) {
  map.setView([lat, lng], 14)

  tambahinMarker(map, lat + 0.005, lng + 0.008, 'Green Hub Center', 'Plastik, Kaca, Kertas · Buka 08-17')
  tambahinMarker(map, lat - 0.007, lng + 0.003, 'City Recycle Point', 'Logam, E-Waste · Buka 09-16')
  tambahinMarker(map, lat + 0.003, lng - 0.009, 'West Drop Off', 'Plastik, Kertas · Pickup terjadwal')
  tambahinMarker(map, lat - 0.004, lng - 0.005, 'Eco Station', 'Semua jenis · Buka 24 jam')
}

onMounted(() => {
  const map = L.map('map').setView([defaultLat, defaultLng], 13)

  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: '© OpenStreetMap'
  }).addTo(map)

  if (navigator.geolocation) {
    navigator.geolocation.getCurrentPosition(
      (pos) => loadMap(map, pos.coords.latitude, pos.coords.longitude),
      () => loadMap(map, defaultLat, defaultLng)
    )
  } else {
    loadMap(map, defaultLat, defaultLng)
  }
})

</script>

<template>
  <section class="max-w-6xl py-20 px-12 mx-auto">
    <div class="justify-between flex gap-8 mb-10">
      <h2 class="text-4xl font-bold max-w-sm leading-tight ">
        Everything you need, in one place.
      </h2>
      <p class="text-gray-500 pt-2 text-base leading-relaxed max-w-md">
        Find nearby recycling locations, supported materials, directions, schedules, 
        and sustainability information through a clean and accessible experience.
      </p>
    </div>
    <div id="map" class="w-full h-[480px] rounded-2xl overflow-hidden z-0"></div>
  </section>
</template>