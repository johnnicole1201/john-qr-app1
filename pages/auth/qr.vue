<template>
  <v-container class="text-center">
    <h1>📷 QR Code Scanner</h1>


    <!-- QR Camera Stream -->
    <qrcode-stream @decode="onDecode" @init="onInit"></qrcode-stream>

    <v-alert v-if="error" type="error" dense>{{ error }}</v-alert>
<style scoped>
.qr-camera {
  width: 50px;     /* lapad ng camera */
  height: 50px;    /* taas ng camera */
  border: 3px solid #4caf50;
  border-radius: 8px;
  margin: auto;
  display: block;
  object-fit: cover; /* para hindi distorted */
}
</style>

    <!-- Result -->
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
  middleware: 'auth', // ✅ para protektado ng Google Auth mo
  data() {
    return {
      result: null,
      error: null
    }
  },
  methods: {
    onDecode(content) {
      this.result = content
    },
    onInit(promise) {
      promise.catch(err => {
        this.error = err.message || 'Camera initialization failed'
      })
    }
  }
}
</script>

<style>
qrcode-stream {
  width: 100%;
  max-width: 400px;
  margin: auto;
}
</style>
