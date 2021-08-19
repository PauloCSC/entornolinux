<template>
  <footer
    v-if="$slidev.nav.currentLayout !== 'cover'"
  >
   <div class="absolute bottom-0 p-2"> By Joseph M. & Paulo S. </div> 
   <div class="absolute bottom-0 right-0 p-2"> {{ $slidev.nav.currentPage }} / {{ $slidev.nav.total }}</div>
    
  </footer>
</template>