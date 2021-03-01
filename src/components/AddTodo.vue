<template>
  <form @submit="onSubmit" class="add-form">
    <div class="form-control">
      <label>Todo</label>
      <input type="text" v-model="text" name="text" placeholder="Add Todo" />
    </div>
    <!-- {{text}} two-way-binding-->
    <div class="form-control">
      <label>Day & Time</label>
      <input
        type="text"
        v-model="day"
        name="day"
        placeholder="Add Day & Time"
      />
    </div>
    <div class="form-control form-control-check">
      <label>Set Reminder</label>
      <input type="checkbox" v-model="reminder" name="reminder" />
    </div>

    <input type="submit" value="Save Todo" class="btn" />
  </form>
</template>

<script>
export default {
  name: 'AddTodo',
  data() {
    return {
      text: '',
      day: '',
      reminder: false,
    }
  },
  methods: {
    onSubmit(e) {
      e.preventDefault()

      if(!this.text) {
        alert('Please add a Todo')
        return
      }
      const newTodo = {
        // id: Math.floor(Math.random() * 100000),
        text: this.text,
        day: this.day,
        reminder: this.reminder
      }
      this.$emit('add-todo', newTodo)

      this.text = ''
      this.day = ''
      this.reminder = false
    }
  }
}
</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
}
.form-control {
  margin: 20px 0;
}
.form-control label {
  display: block;
  margin-left: 5px;
}
.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}
.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.form-control-check label {
  flex: 1;
}
.form-control-check input {
  flex: 2;
  height: 20px;
}
.btn {
  width: 100%;
  background: rgb(46, 148, 85);
}

</style>