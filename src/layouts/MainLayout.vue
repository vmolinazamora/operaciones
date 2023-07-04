<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-toolbar-title> Operaciones App </q-toolbar-title>

        <div>Quasar v{{ $q.version }}</div>
      </q-toolbar>
    </q-header>

    <q-page-container class="page">
      <router-view />
    </q-page-container>

    <waves-effect :waves="config" class="fixed-bottom"></waves-effect>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from "vue";
import WavesEffect from "src/components/WavesEffect.vue";

export default defineComponent({
  name: "MainLayout",
  components: { WavesEffect },
  setup() {
    const nombre = ref(null);
    const config = ref({
      color: { r: 255, g: 255, b: 255 },
      waves: [
        { x: 48, y: 0, delay: -2, duration: 7 },
        { x: 48, y: 3, delay: -3, duration: 10 },
        { x: 48, y: 5, delay: -4, duration: 13 },
        { x: 48, y: 7, delay: -5, duration: 20 },
      ],
    });

    return {
      nombre,
      config,
    };
  },
});
</script>
