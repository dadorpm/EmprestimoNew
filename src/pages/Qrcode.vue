<template>
  <q-page class="flex column flex-center">
    <h4 class="">Sistema de Geração de QR-Code</h4>
    <div class="q-pa-md">
      <div class="q-gutter-md" style="max-width: 600px">
        <q-input square outlined type="text" v-model="url" label="Digite a url aqui" width="600px" />
      </div>
    </div>
    <br /><br />
    <qrcode-svg v-if="url" :id="uid" :value="url" size="300" />
    <q-btn v-if="url" class="q-mt-xl" color="amber" glossy label="Baixar Qr-code" @click="downloadPNG" />
  </q-page>
</template>

<script>
import { QrcodeSvg } from 'qrcode.vue'

export default {
  components: { QrcodeSvg },
  data() {
    return {
      url: null,
      uid: 'qrcode',
    };
  },
  methods:{
    downloadPNG(){
      const svgElement = document.getElementById('qrcode');
      const svgString = new XMLSerializer().serializeToString(svgElement);
      const svgBase64 = window.btoa(unescape(encodeURIComponent(svgString)));
      const image = new Image();
      image.onload = function () {
        const canvas = document.createElement('canvas');
        canvas.width = svgElement.getBoundingClientRect().width;
        canvas.height = svgElement.getBoundingClientRect().height;
        const context = canvas.getContext('2d');
        context.drawImage(image, 0, 0);
        const downloadLink = document.createElement('a');
        downloadLink.href = canvas.toDataURL('image/png');
        downloadLink.download = 'qrcode.png';
        document.body.appendChild(downloadLink);
        downloadLink.click();
        document.body.removeChild(downloadLink);
      };
      image.src = 'data:image/svg+xml;base64,' + svgBase64;
    }
  }
};
</script>
