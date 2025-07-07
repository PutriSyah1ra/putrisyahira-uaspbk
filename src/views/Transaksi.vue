<template>
  <div class="p-4">
    <!-- Judul & Keranjang -->
    <div class="flex justify-between items-center mb-2">
      <div>
        <h1 class="text-2xl font-bold text-green-700">Transaksi</h1>
        <p class="text-sm text-green-600 italic">Segarkan harimu dengan jus pilihan!</p>
      </div>

      <!-- Indikator Keranjang -->
      <RouterLink to="/keranjang" class="relative inline-block">
        <span class="bg-green-600 text-white px-3 py-1 rounded-full shadow">
          🛒 Keranjang
          <span
            v-if="totalItem > 0"
            class="ml-2 inline-flex items-center justify-center w-5 h-5 text-xs font-bold text-green-600 bg-white rounded-full"
          >
            {{ totalItem }}
          </span>
        </span>
      </RouterLink>
    </div>

    <!-- Search -->
    <input
      v-model="keyword"
      type="text"
      placeholder="Cari menu jus segar..."
      class="w-full md:w-1/3 p-2 border rounded mb-4 focus:outline-none focus:ring-2 focus:ring-green-500 border-green-300"
    />

    <!-- Grid Menu -->
    <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 gap-4">
      <div
        v-for="item in hasilPencarian"
        :key="item.id"
        class="bg-white rounded-lg shadow p-4 hover:shadow-md transition border border-green-100"
      >
        <h2 class="font-semibold text-lg text-green-700">{{ item.nama }}</h2>
        <p class="text-sm text-gray-500 mb-2">Rp {{ item.harga.toLocaleString() }}</p>
        <button
          @click="transaksiStore.tambahKeKeranjang(item)"
          class="bg-green-600 hover:bg-green-700 text-white px-4 py-1 rounded text-sm transition duration-150 ease-in-out"
        >
          Tambah
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'
import { RouterLink } from 'vue-router'
import { useMenuStore } from '@/stores/menuStore'
import { useTransaksiStore } from '@/stores/transaksiStore'

const menuStore = useMenuStore()
const transaksiStore = useTransaksiStore()

const keyword = ref('')

onMounted(() => {
  menuStore.fetchMenu()
})

const hasilPencarian = computed(() =>
  keyword.value
    ? menuStore.cariMenu(keyword.value)
    : menuStore.daftarMenu
)

const totalItem = computed(() => transaksiStore.totalItem)
</script>
