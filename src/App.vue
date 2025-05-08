<script setup>
import { ref, computed } from 'vue'

const listTugas = ref([])
const inputTugas = ref('')
const filterTugas = ref('semua')

const tambahTugas = () => {
  if (inputTugas.value.trim() !== '') {
    listTugas.value.push({
      id: listTugas.value.length + 1,
      nama: inputTugas.value,
      status: false
    })
    inputTugas.value = ''
  }
}

function hapusTugas(id) {
  listTugas.value = listTugas.value.filter(tugas => tugas.id !== id)
}

const filterTugasList = computed(() => {
  if (filterTugas.value === 'semua') {
    return listTugas.value
  } else if (filterTugas.value === 'selesai') {
    return listTugas.value.filter(tugas => tugas.status === 'Selesai')
  } else if (filterTugas.value === 'belum-selesai') {
    return listTugas.value.filter(tugas => tugas.status === 'Belum Selesai')
  }
})

</script>

<template>
  <div>
    <h1>Daftar Tugas Kuliah</h1>
    <input type="text" v-model="inputTugas" @keyup.enter="tambahTugas" placeholder="Tambah tugas baru">
    <button @click="tambahTugas">Tambah</button>
    <div>
      <button @click="filterTugas = 'semua'">Semua</button>
      <button @click="filterTugas = 'selesai'">Selesai</button>
      <button @click="filterTugas = 'belum-selesai'">Belum Selesai</button>
    </div>

    <ul>
      <li v-for="tugas in filterTugasList" :key="tugas.id">
        <input type="checkbox" v-model="tugas.status">
        {{ tugas.nama }} - {{ tugas.status }}
        <button @click="hapusTugas(tugas.id)">Hapus</button>
      </li>
    </ul>
  </div>
</template>

<style scoped></style>
