<template>
  <nav>
    <ToDoApp />
  </nav>
  <router-view/>
</template>




<script>
import ToDoApp from './components/ToDoApp.vue'
export default {
  name: 'APP',

  components:{
ToDoApp,
   },
}
</script>

<style lang="scss">
</style>
