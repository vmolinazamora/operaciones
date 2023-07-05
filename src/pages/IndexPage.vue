<template>
  <q-page class="flex flex-center">
    <q-card style="width: 600px" class="q-pa-md text-center">
      <div class="row">
        <div class="col">
          <div class="text-h4">Ingresa tu nombre</div>
          <p>
            <q-input
              ref="nombreRef"
              v-model.trim="nombre"
              class="text-uppercase text-h3"
              input-class="text-center"
              maxlength="18"
              counter
              :rules="[(val) => !!val || 'Nombre es obligatorio']"
              @keyup.enter.prevent="siguiente"
            >
              <template v-slot:after>
                <q-btn
                  round
                  flat
                  icon="fingerprint"
                  size="xl"
                  color="black"
                  @click="siguiente"
                /> </template
            ></q-input>
          </p>
        </div>
      </div>
    </q-card>
  </q-page>
</template>

<script>
import { defineComponent, ref } from "vue";
import { useQuasar } from "quasar";
import { useRouter } from "vue-router";

export default defineComponent({
  name: "IndexPage",

  setup() {
    const $q = useQuasar();
    const $router = useRouter();
    const nombre = ref("");
    const nombreRef = ref(null);

    function siguiente() {
      nombreRef.value.validate();
      if (!nombreRef.value.hasError) {
        $q.localStorage.set("nombre", nombre.value.toUpperCase());
        $router.replace("/juego");
      }
    }

    return { nombre, nombreRef, siguiente };
  },
});
</script>
