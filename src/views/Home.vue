<template>
<div>
  <AddTodo v-show="showAddTodo" @add-todo="addTodo" />
  <Todos @toggle-reminder="toggleReminder" @delete-todo="deleteTodo" :todos="todos" />
</div>
  
</template>

<script>
import AddTodo from '../components/AddTodo.vue'
import Todos from '../components/Todos'

export default {
  name: 'Home',
  props: {
    showAddTodo: Boolean,
  },
  components: {
    Todos,
    AddTodo
  },
  data() {
    return {
      todos: []
    }
  },
  methods: {

    // lägg till i databasen
    async addTodo(todo){
       const res = await fetch('api/todos', {
         method: 'POST',
         headers: {
           'Content-type': 'application/json',
         },
         body: JSON.stringify(todo)
       })

      const data = await res.json()
      this.todos = [...this.todos, data]
    },

    // ta bort från databasen
    async deleteTodo(id) {
      if(confirm('Är du säker på att du vill ta bort?')) {
        const res = await fetch(`api/todos/${id}`, {
          method: 'DELETE'
        })
        res.status === 200 ? ( this.todos = this.todos.filter((todo) => todo.id !== id)) :
        alert('Kunde inte ta bort Todo')

       
      }
    },

    // uppdatera toggle-funktionen i databasen
    async toggleReminder(id) {
      const todoToToggle = await this.fetchTodo(id)
      const updTodo = {...todoToToggle, reminder: !todoToToggle.reminder}

      const res = await fetch(`api/todos/${id}`, {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(updTodo)
      })

      const data = await res.json()

      // console.log(id) 
      this.todos = this.todos.map((todo) => todo.id === id ? {...todo, reminder: data.reminder} : todo)
    },



    // koppla ihop med databasen
    async fetchTodos() {
      const res = await fetch('api/todos')

      const data = await res.json()
      return data
    },
    // hämta en specifik todo
    async fetchTodo(id) {
    const res = await fetch(`api/todos/${id}`)  

      const data = await res.json()
      return data
    },
  },

  async created() {
    this.todos = await this.fetchTodos()
  }
}
</script>

<style>

</style>