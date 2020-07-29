<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <a class="navbar-brand" href="/">Nuxt SSR</a>
    <button
      class="navbar-toggler"
      type="button"
      data-toggle="collapse"
      data-target="#navbarSupportedContent"
      aria-controls="navbarSupportedContent"
      aria-expanded="false"
      aria-label="Toggle navigation"
    >
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav mr-auto">
        <li class="nav-item">
          <nuxt-link class="nav-link" exact no-prefetch active-class="active" to="/">Home</nuxt-link>
        </li>
        <li class="nav-item">
          <nuxt-link class="nav-link" no-prefetch active-class="active" to="/about">About</nuxt-link>
        </li>
        <li class="nav-item">
          <nuxt-link class="nav-link" no-prefetch active-class="users" to="/users">Users</nuxt-link>
        </li>
        <li class="nav-item" v-if="!hasToken">
          <nuxt-link class="nav-link" no-prefetch active-class="login" to="/login">Login</nuxt-link>
        </li>
        <li class="nav-item" v-else>
          <a class="nav-link" @click.prevent="logout" href="#">Logout</a>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
export default {
  computed: {
    hasToken() {
      return this.$store.getters.hasToken
    }
  },
  methods: {
    logout() {
      this.$router.dispatch('logout')
      this.$router.push('/login')
    }
  }
}
</script>