<template>
  <footer 
  v-if="$slidev.nav.currentPage == 1"
  class="absolute top-0 left-0 p-2">
      <img class="h-12" src="https://box.misaelabanto.com/logo_nixvoid.png">
  </footer>
  <footer 
  v-else
  class="absolute top-0 right-0 p-2">
      <img class="h-12" src="https://box.misaelabanto.com/logo_nixvoid.png">
  </footer>
</template>
