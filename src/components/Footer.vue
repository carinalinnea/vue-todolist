<template>
  <footer>
    <p>Copyright &copy; cawebdev 2021</p>
     <router-link to="/about" class="about">About</router-link>
  </footer>
</template>

<script>
export default {

}
</script>

<style scoped>
footer {
  margin-top: 25px;
  text-align: center;
}
p {
  margin-bottom: 0.5rem;
}
.about {
  color: rgb(46, 148, 85);
  background: #fff;
  border: 1px solid rgb(46, 148, 85);
  padding: 0 1rem;
  border-radius: 5px;
}
</style>