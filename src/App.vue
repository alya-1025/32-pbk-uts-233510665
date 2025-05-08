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
    return listTugas.value.filter(tugas => tugas.status)
  } else if (filterTugas.value === 'belum-selesai') {
    return listTugas.value.filter(tugas => !tugas.status)
  }
})

</script>

<template>
  <div class="h-screen flex bg-gradient-to-r from-rose-100 to-pink-100 font-sans">
    <aside class="w-1/3 bg-pink-200 p-6 shadow-md flex flex-col justify-between">
      <div>
        <h1 class="text-2xl font-bold text-center mb-6 text-rose-900">Tugas Kuliah</h1>
        <input v-model="inputTugas" @keyup.enter="tambahTugas" placeholder="Tambah tugas baru"
          class="w-full px-4 py-2 mb-3 rounded border border-pink-400 focus:outline-none focus:ring-2 focus:ring-pink-500" />
        <button @click="tambahTugas" class="w-full bg-pink-600 text-white py-2 rounded hover:bg-pink-700 transition">
          Tambah
        </button>
      </div>

      <div class="mt-8 space-y-3">
        <button @click="filterTugas = 'semua'" :class="filterTugas === 'semua' ? activeBtn : defaultBtn"
          class="w-full py-2 rounded-md font-medium transition duration-200 shadow-md">
          Semua
        </button>

        <button @click="filterTugas = 'selesai'" :class="filterTugas === 'selesai' ? activeBtn : defaultBtn"
          class="w-full py-2 rounded-md font-medium transition duration-200 shadow-md">
          Selesai
        </button>

        <button @click="filterTugas = 'belum-selesai'" :class="filterTugas === 'belum-selesai' ? activeBtn : defaultBtn"
          class="w-full py-2 rounded-md font-medium transition duration-200 shadow-md">
          Belum Selesai
        </button>
      </div>
    </aside>

    <main class="w-2/3 p-6 overflow-y-auto">
      <ul class="space-y-4 pb-24">
        <li v-for="tugas in filterTugasList" :key="tugas.id"
          class="flex justify-between items-center bg-white shadow rounded-lg p-4 border-l-4 border-pink-300">
          <div class="flex items-center gap-3 w-full">
            <input type="checkbox" v-model="tugas.status" class="accent-pink-500 w-5 h-5" />
            <span :class="tugas.status ? 'line-through text-gray-500' : ''" class="text-lg flex-1">
              {{ tugas.nama }}
            </span>
          </div>
          <button @click="hapusTugas(tugas.id)"
            class="bg-rose-400 hover:bg-rose-500 text-white px-3 py-1 rounded transition">
            Hapus
          </button>
        </li>
      </ul>
    </main>
  </div>
</template>

<style scoped></style>
