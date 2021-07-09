<template>
  <div>

    <div class="headerbox">
      <Header/>
    </div>

    <Tasklist/>
  
  </div>
</template>

<script>

import Header from './Header.vue';
import Tasklist from './Tasklist.vue';

export default {
  name: 'Dashboard',
  components: {
    Header,
    Tasklist
  }
}

</script>


<style scoped>

.headerbox{
  background: lightblue;
  margin: 0 13em;
  border-top-left-radius: 1em;  
  border-top-right-radius: 1em;
}

</style>