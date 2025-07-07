<template>
  <div class="fixed top-0 left-0 h-screen w-48 bg-green-600 text-white flex flex-col shadow-lg">
    <div class="p-4 text-2xl font-bold border-b border-white">
      Syahira Jus
    </div>

    <nav class="flex-1 mt-4">
      <RouterLink
        to="/"
        class="block px-4 py-2 hover:bg-green-700"
        :class="{ 'bg-green-800': $route.name === 'transaksi' }"
      >
        Transaksi
      </RouterLink>

      <RouterLink
        to="/keranjang"
        class="block px-4 py-2 hover:bg-green-700"
        :class="{ 'bg-green-800': $route.name === 'keranjang' }"
      >
        Keranjang
      </RouterLink>

      <RouterLink
        to="/riwayat"
        class="block px-4 py-2 hover:bg-green-700"
        :class="{ 'bg-green-800': $route.name === 'profile' }"
      >
        Riwayat
      </RouterLink>

      <RouterLink
        to="/laporan"
        class="block px-4 py-2 hover:bg-green-700"
        :class="{ 'bg-green-800': $route.name === 'laporan' }"
      >
        Laporan
      </RouterLink>
    </nav>
  </div>
</template>

<script setup>
import { RouterLink, useRoute } from 'vue-router'
const route = useRoute()
</script>

<style scoped>
.router-link-exact-active {
  font-weight: bold;
}

/* Tambahan opsional untuk tema segar */
nav a {
  transition: background-color 0.2s ease;
}
</style>
