<script setup>
import { ref } from 'vue'

const listTugas = ref([])
const inputTugas = ref('')

const tambahTugas = () => {
  if (inputTugas.value.trim() !== '') {
    listTugas.value.push({
      id: listTugas.value.length + 1,
      nama: inputTugas.value,
      status: 'Belum Selesai'
    })
    inputTugas.value = ''
  }
}

</script>

<template>
  <div>
    <h1>Daftar Tugas Kuliah</h1>
    <input type="text" v-model="inputTugas" @keyup.enter="tambahTugas" placeholder="Tambah tugas baru">
    <button @click="tambahTugas">Tambah</button>
  </div>
</template>

<style scoped>

</style>
