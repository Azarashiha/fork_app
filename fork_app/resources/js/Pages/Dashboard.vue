<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head } from '@inertiajs/vue3';
import { GoogleMap } from 'vue3-google-map';
import { ref, onMounted } from 'vue';

const center = ref({ lat: 35.6812, lng: 139.7671 });
const zoom = ref(12);
const apiKey = import.meta.env.VITE_GOOGLE_MAPS_API_KEY;
const mapRef = ref(null);

onMounted(() => {
  if (mapRef.value) {
    const { map } = mapRef.value;
    const advancedMarker = new window.google.maps.marker.AdvancedMarkerElement({
      map,
      position: center.value,
    });
  }
});
</script>

<template>
  <Head title="Dashboard" />

  <AuthenticatedLayout>
    <template #header>
      <h2 class="font-semibold text-xl text-gray-800 leading-tight">Dashboard</h2>
    </template>

    <div class="py-12">
      <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
        <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
          <div class="p-6 text-gray-900">
            <h3 class="text-lg font-semibold mb-4">Google Map</h3>
            <div class="map-container">
              <GoogleMap
                :api-key="apiKey"
                :center="center"
                :zoom="zoom"
                class="full-screen-map"
                @map-ready="mapRef = $event"
              />
            </div>
          </div>
        </div>
      </div>
    </div>
  </AuthenticatedLayout>
</template>

<style scoped>
.py-12 {
  padding-top: 1rem;
  padding-bottom: 1rem;
}

.map-container {
  width: 100%;
  height: calc(100vh - 180px); /* ヘッダーとその他の要素の高さを考慮 */
  min-height: 400px; /* 最小高さを設定 */
}

.full-screen-map {
  width: 100%;
  height: 100%;
}

@media (max-width: 640px) {
  .py-12 {
    padding-top: 0.5rem;
    padding-bottom: 0.5rem;
  }

  .map-container {
    height: calc(100vh - 150px); /* スマホ向けに高さを調整 */
  }

  .p-6 {
    padding: 1rem;
  }
}
</style>