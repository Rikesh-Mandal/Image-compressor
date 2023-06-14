<template>
  <div>
    <input type="file" ref="imageInput" @change="onFileChange">
    <button @click="compressImage" :disabled="!selectedFile">Compress</button>
    <img :src="compressedImage" v-if="compressedImage">
  </div>
</template>

<script>
import Compressor from 'compressorjs';

export default {
  data() {
    return {
      selectedFile: null,
      compressedImage: null,
    };
  },
  methods: {
    onFileChange(event) {
      this.selectedFile = event.target.files[0];
    },
    compressImage() {
      if (!this.selectedFile) {
        return;
      }

      new Compressor(this.selectedFile, {
        quality: 0.1, // Adjust the desired image quality (0.1 to 1)
        maxWidth: 800, // Adjust the maximum width of the image
        maxHeight: 800, // Adjust the maximum height of the image
        success: (compressedFile) => {
          const reader = new FileReader();
          reader.readAsDataURL(compressedFile);

          reader.onload = () => {
            this.compressedImage = reader.result;
          };
        },
        error: (error) => {
          console.log('Compression error:', error.message);
        },
      });
    },
  },
};
</script>

<style scoped>
</style>
