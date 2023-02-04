<script setup>
import { RouterLink, RouterView } from 'vue-router'
import socialicon from './components/social.vue'

</script>

<template>
  <header>
    <nav class="navbar navbar-expand-none bg-white  w-100" data-bs-theme="dark">
  <div class="container">
    <div class="w-100 d-flex justify-content-between align-items-center">


<socialicon color="c1" />

    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>

    </div>
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav me-auto mb-2 mb-lg-0  text-end text-white">
        <li class="nav-item mt-3">
            <RouterLink class="nav-link" to="/">Home</RouterLink>
        </li>
        <li class="nav-item">
            <RouterLink class="nav-link" to="/about">About</RouterLink>
        </li>
      </ul>

    </div>
  </div>
</nav>

  </header>

  <RouterView />
</template>

<style scoped>

</style>
