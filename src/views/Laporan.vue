<template>
  <div class="p-4">
    <h1 class="text-2xl font-bold text-green-700 mb-4">Laporan Penjualan</h1>

    <!-- Ringkasan -->
    <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
      <div class="bg-green-50 p-4 rounded-lg shadow border border-green-100 flex items-center justify-between">
        <div>
          <p class="text-sm text-green-700 font-medium">📊 Total Transaksi</p>
          <p class="text-2xl font-bold text-green-800">{{ jumlahTransaksi }}</p>
        </div>
      </div>

      <div class="bg-green-50 p-4 rounded-lg shadow border border-green-100 flex items-center justify-between">
        <div>
          <p class="text-sm text-green-700 font-medium">💰 Total Pemasukan</p>
          <p class="text-2xl font-bold text-green-800">
            Rp {{ totalPemasukan.toLocaleString() }}
          </p>
        </div>
      </div>
    </div>

    <!-- Rekap Transaksi -->
    <div v-if="riwayat.length > 0">
      <h2 class="text-lg font-semibold text-green-700 mb-2">Rekap Transaksi</h2>
      <div class="space-y-4">
        <div
          v-for="trx in riwayat.slice().reverse()"
          :key="trx.id"
          class="bg-white p-4 rounded-lg shadow-sm border border-gray-100 hover:border-green-300 transition"
        >
          <div class="flex justify-between items-start">
            <div>
              <p class="font-semibold text-green-700">ID: {{ trx.id }}</p>
              <p class="text-sm text-gray-500">Tanggal: {{ formatTanggal(trx.tanggal) }}</p>
            </div>
            <p class="font-bold text-green-700 text-right">
              Rp {{ hitungTotal(trx.pesanan).toLocaleString() }}
            </p>
          </div>
        </div>
      </div>
    </div>

    <!-- Kosong -->
    <div v-else class="text-gray-500 mt-8 text-center">
      Tidak ada transaksi untuk dilaporkan 📭
    </div>
  </div>
</template>

<script setup>
import { onMounted, computed } from 'vue'
import { useTransaksiStore } from '@/stores/transaksiStore'

const transaksiStore = useTransaksiStore()

onMounted(() => {
  transaksiStore.fetchRiwayat()
})

const riwayat = computed(() => transaksiStore.riwayat)

const jumlahTransaksi = computed(() => riwayat.value.length)

const totalPemasukan = computed(() =>
  riwayat.value.reduce((sum, trx) => {
    return sum + trx.pesanan.reduce((s, item) => s + item.harga * item.jumlah, 0)
  }, 0)
)

const hitungTotal = (pesanan) =>
  pesanan.reduce((sum, item) => sum + item.harga * item.jumlah, 0)

const formatTanggal = (iso) => {
  const d = new Date(iso)
  return d.toLocaleString('id-ID', {
    day: '2-digit',
    month: 'long',
    year: 'numeric',
    hour: '2-digit',
    minute: '2-digit'
  })
}
</script>
