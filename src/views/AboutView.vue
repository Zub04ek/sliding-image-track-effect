<script setup lang="ts">
import { RouterLink } from 'vue-router'
import HelloWorld from '../components/HelloWorld.vue'
</script>

<template>
  <div id="container" class="max-w-[1280px] p-[2rem]">
    <header>
      <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />

      <div class="wrapper">
        <HelloWorld msg="You did it!" />

        <nav class="flex flex-wrap gap-3">
          <RouterLink class="w-[calc((100%_-36px)/4)]" to="/">Home</RouterLink>
          <RouterLink class="w-[calc((100%_-36px)/4)]" to="/about">About</RouterLink>
          <RouterLink class="w-[calc((100%_-36px)/4)]" to="/slider">Slider</RouterLink>
          <RouterLink class="w-[calc((100%_-36px)/4)]" to="/counter">Counter</RouterLink>
          <RouterLink class="w-[calc((100%_-36px)/4)]" to="/notes">Notes</RouterLink>
        </nav>
      </div>
    </header>
    <main class="about">
      <h1>This is an about page</h1>
    </main>
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
  #container {
    display: grid;
    grid-template-columns: 1fr 1fr;
    padding: 0 2rem;
    margin: 0 auto;
  }
}
</style>
