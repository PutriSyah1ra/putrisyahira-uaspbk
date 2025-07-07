<template>
  <div class="p-4">
    <h1 class="text-2xl font-bold text-green-700 mb-4">Keranjang</h1>

    <!-- Kosong -->
    <div v-if="keranjang.length === 0" class="text-gray-500 text-center mt-8">
      <p class="text-lg">Keranjang masih kosong 🛒</p>
      <p class="text-sm text-green-600 italic">Yuk pilih jus segar favoritmu!</p>
    </div>

    <!-- Daftar Item -->
    <div v-else class="space-y-4">
      <div
        v-for="item in keranjang"
        :key="item.id_menu"
        class="flex items-center justify-between bg-white shadow rounded p-4 border border-green-100"
      >
        <div>
          <h2 class="font-semibold text-green-700">{{ item.nama_menu }}</h2>
          <p class="text-sm text-gray-500">Rp {{ item.harga.toLocaleString() }} x {{ item.jumlah }}</p>
        </div>
        <div class="text-right">
          <p class="font-bold text-green-700">Rp {{ (item.harga * item.jumlah).toLocaleString() }}</p>
          <button
            @click="hapusItem(item.id_menu)"
            class="mt-1 text-xs text-red-600 hover:underline"
          >
            Hapus
          </button>
        </div>
      </div>

      <!-- Total & Checkout -->
      <div class="text-right mt-6">
        <p class="text-lg font-bold mb-2 text-green-700">
          Total: Rp {{ totalHarga.toLocaleString() }}
        </p>
        <button
          @click="checkout"
          class="bg-green-600 hover:bg-green-700 text-white px-6 py-2 rounded shadow transition"
        >
          Checkout
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'
import { useTransaksiStore } from '@/stores/transaksiStore'
import { useRouter } from 'vue-router'

const router = useRouter()
const transaksiStore = useTransaksiStore()

const keranjang = computed(() => transaksiStore.keranjang)
const totalHarga = computed(() => transaksiStore.totalHarga)

const hapusItem = (id_menu) => {
  transaksiStore.hapusDariKeranjang(id_menu)
}

const checkout = async () => {
  await transaksiStore.checkout()
  alert('Checkout berhasil!')
  router.push('/')
}
</script>
