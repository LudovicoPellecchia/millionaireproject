

<script>
import ContenitoreComp from './components/ContenitoreComp.vue';

export default {
  components: {
    ContenitoreComp
  },

  data() {
    return {

    }
  }
}
</script>


<template>
  <div class="container">
    <h1 class="text-center title">Chi vuole essere milionario</h1>
    <ContenitoreComp></ContenitoreComp>
  </div>
</template>

<style lang="scss">
.title{
  margin-top: 150px;
  margin-bottom: 100px;
}


</style>
