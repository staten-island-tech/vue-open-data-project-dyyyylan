<script setup>
import { RouterLink, RouterView } from 'vue-router'

</script>

<template>
  <header>
    <div class="wrapper">
      <HelloWorld msg="You did it!" />

      <nav>
        <RouterLink to="/malechart">Malechart</RouterLink>
        <RouterLink to="/">Female Chart</RouterLink>
        <RouterLink to="/about">Female</RouterLink>
        <RouterLink to="/male">Male</RouterLink>

      </nav>
    </div>
  </header>

  <RouterView />
</template>        

<style scoped>

</style>
