<template>
  <q-page class="flex column flex-center">
    <h4 class="">Sistema de Geração de QR-Code</h4>
    <div class="q-pa-md">
      <div class="q-gutter-md" style="max-width: 600px">
        <q-input square outlined type="text" v-model="url" label="Digite a url aqui" width="600px" />
      </div>
    </div>
    <br /><br />
    <qrcode-vue v-if="url" :value="url" size="300" />
  </q-page>
</template>

<script>
import QrcodeVue from "qrcode.vue";

export default {
  components: { QrcodeVue },
  data() {
    return {
      url: null,
    };
  },
};
</script>