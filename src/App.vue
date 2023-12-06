

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
    <div class="text-center transform ">
      <h1 class="title">DO YOUR QUIZ!</h1>
    </div>
    <ContenitoreComp></ContenitoreComp>
  </div>
</template>

<style lang="scss">
.transform {
  transform: skewY(-4deg);
}

.title {
  transition: text-decoration 0.4s;
  letter-spacing: 10px;
  font-size: 5rem;
  text-shadow: 3px 7px #311847;
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
  color: white;
  display: inline-block;
  margin-bottom: 80px;
  border-radius: 40px;
  padding: 20px 40px;
  /*   box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
 */

  &:hover {
    text-decoration: dashed underline;

  }
}
</style>
