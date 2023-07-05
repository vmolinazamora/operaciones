<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-toolbar-title> OPERACIONES APP </q-toolbar-title>
        <div class="text-h5">
          {{
            ($q.localStorage.getItem("nombre") ? "JUGADOR ACTIVO: " : "") +
            $q.localStorage.getItem("nombre")
          }}
        </div>

        <q-space></q-space>
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
import { useQuasar } from "quasar";
import { useRouter } from "vue-router";

export default defineComponent({
  name: "MainLayout",
  components: { WavesEffect },
  setup() {
    const $q = useQuasar();
    const $router = useRouter();
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

    $router.beforeEach((to, from, next) => {
      // ...
      // explicitly return false to cancel the navigation
      if (to.path === "/juego" && $q.localStorage.getItem("nombre")) {
        next();
      } else {
        //console.log(to, from);
        return false;
      }
    });

    if (
      $router.currentRoute.value.path === "/" &&
      $q.localStorage.getItem("nombre")
    ) {
      $router.replace("/juego");
    }

    return {
      nombre,
      config,
    };
  },
});
</script>
