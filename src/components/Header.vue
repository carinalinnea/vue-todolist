<template>
  <header>
    <h1>{{title}}</h1>
    <Button v-show="homePage" @btn-click="$emit('toggle-add-todo')" :text="showAddTodo ? 'Close' : 'Add Todo'" :color="showAddTodo ? 'red' : 'green' "/>
  </header>
</template>

<script>
import Button from './Button'

export default {
  name: 'Header',
  props: {
    title: String,
    showAddTodo: Boolean,
  },
  components: {
    Button,
  },
  computed: {
    homePage() {
      if(this.$route.path === '/') {
        return true
      } else {
        return false
      }
    }
  }
}
</script>

<style scoped>
  header{
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 20px;
    background: rgb(213, 245, 200);
    border-radius: 5px;
  }
  h1 {
  color: rgb(20, 87, 34);
}
</style>