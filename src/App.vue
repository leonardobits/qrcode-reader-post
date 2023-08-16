<template>
  <div class="scanner-container d-flex align-items-center justify-content-center">
    <b-card class="scanner-card mt-4 mb-4">
      <b-card-title class="text-center scanner-title" style="font-size: 1.5rem; margin-top: 1rem;">Scanner de Código QR</b-card-title>
      <div class="text-right" style="margin-top: -1.5rem; margin-right: 1rem;">
        <b-button variant="link" @click="openSettingsModal">
          <box-icon name='cog' type='solid'></box-icon>
        </b-button>
      </div>
      <b-card-text class="text-center scanner-text" style="margin-top: 0.5rem;">
        Aponte a câmera para o código QR para iniciar a leitura.
      </b-card-text>
      <b-card-body class="scanner-preview" style="margin-top: 1rem;">
        <qrcode-stream :key="count" @decode="onDecode" @init="onInit">
          <template #preview>
            <div class="scanner-loading d-flex justify-content-center align-items-center">
              <b-spinner variant="light"></b-spinner>
            </div>
          </template>
        </qrcode-stream>
      </b-card-body>
    </b-card>
    <b-modal v-model="settingsModal" title="Configurações">
      <b-form-group label="Endereço URL de Destino">
        <b-form-input v-model="destinationUrl"></b-form-input>
      </b-form-group>
    </b-modal>
  </div>
</template>

<script>
import { QrcodeStream } from 'qrcode-reader-vue3'

export default {
  components: {
    QrcodeStream
  },
  data() {
    return {
      count: 0,
      settingsModal: false,
      destinationUrl: ''
    }
  },
  methods: {
showAlert(text) {
    this.$swal({
        title: text,
        toast: true,
        position: 'bottom-end',
        showConfirmButton: false,
        timer: 3000,
        icon: "success",
    });
},
    onDecode(result) {
      this.showAlert(result);
      this.count += 1;
    },
    onInit(promise) {
      promise.then(() => {
        console.log('Componentes prontos!')
      })
    },
    openSettingsModal() {
      this.settingsModal = true;
    },
    saveSettings() {
      this.settingsModal = false;
    },
  }
}
</script>
<style>
  body {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  }
</style>
