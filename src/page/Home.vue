<template>
  <div>
      Home
      <button @click="logout">logout</button>
  </div>
</template>

<script>
    export default {
        name: 'Home',
        methods: {
            logout() {
                this.$router.push('login')
            }
        }
    }
</script>
