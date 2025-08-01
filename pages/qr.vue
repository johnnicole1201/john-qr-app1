<template>
  <v-container class="text-center">
    <h1>📷 QR Code Scanner</h1>

    <div class="camera-box">
      <client-only>
        <qrcode-stream class="qr-camera" @decode="onDecode" @init="onInit" />
      </client-only>
      <div class="scanner-line"></div>
    </div>

    <v-alert v-if="error" type="error" dense>{{ error }}</v-alert>

    <v-card class="mt-4 pa-3" v-if="result">
      <v-card-title>Scanned Result:</v-card-title>
      <v-card-text>
        <v-chip color="green" dark>{{ result }}</v-chip>
      </v-card-text>
    </v-card>
  </v-container>
</template>

<script>
export default {
  data() {
    return { result: null, error: null }
  },
  methods: {
    onDecode(content) { this.result = content },
    onInit(promise) {
      promise.catch(err => { this.error = err.message || 'Camera failed' })
    }
  }
}
</script>

<style scoped>
.camera-box {
  width: 120px;
  height: 120px;
  position: relative;
  overflow: hidden;
  border: 3px solid #4caf50;
  border-radius: 8px;
  margin: auto;
}
.qr-camera >>> video {
  width: 100% !important;
  height: 100% !important;
  object-fit: cover !important;
}
.scanner-line {
  position: absolute;
  width: 100%;
  height: 2px;
  background: red;
  animation: scan 2s infinite;
}
@keyframes scan {
  0% { top: 0; }
  50% { top: 98%; }
  100% { top: 0; }
}
</style>
