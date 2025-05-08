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

function hapusTugas(id) {
  listTugas.value = listTugas.value.filter(tugas => tugas.id !== id)
}

</script>

<template>
  <div>
    <h1>Daftar Tugas Kuliah</h1>
    <input type="text" v-model="inputTugas" @keyup.enter="tambahTugas" placeholder="Tambah tugas baru">
    <button @click="tambahTugas">Tambah</button>

    <ul>
      <li v-for="tugas in listTugas" :key="tugas.id">
        {{ tugas.nama }} - {{ tugas.status }}
        <button @click="hapusTugas(tugas.id)">Hapus</button>
      </li>
    </ul>
  </div>
</template>

<style scoped></style>
