<template>
  <div id="app">
    <div id="header">
      <Header />
    </div>
      <router-view/>
  </div>
</template>

<script>
import Header from '@/components/Header.vue'
export default {
  components:{
    Header,
  }
}
</script>