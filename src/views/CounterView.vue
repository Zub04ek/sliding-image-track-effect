<template>
  <div id="container" class="max-w-[1280px] p-[2rem]">
    <header>
      <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />

      <div class="wrapper">
        <HelloWorld msg="You did it!" />

        <nav class="lg:flex lg:gap-3">
          <RouterLink to="/">Home</RouterLink>
          <RouterLink to="/counter">Counter</RouterLink>
          <RouterLink to="/notes">Notes</RouterLink>
          <RouterLink to="/slider">Slider</RouterLink>
        </nav>
      </div>
    </header>
    <main class="min-h-[50vh] lg:min-h-screen flex items-center flex-col justify-center gap-5">
      <h4 class="text-3xl">The current count is...</h4>
      <div class="flex">
        <button type="button" @click="count--" class="w-[5rem] p-5 rounded-full text-3xl">-</button>
        <div class="relative">
          <!-- <Transition> -->
          <h1 :key="count" class="min-w-[10rem] min-h-[6rem] text-8xl text-center">
            {{ count }}
          </h1>
          <!-- </Transition> -->
        </div>
        <button type="button" @click="count++" class="w-[5rem] p-5 rounded-full text-3xl">+</button>
      </div>
    </main>
  </div>
</template>

<script setup lang="js">
import { ref } from 'vue'
import { RouterLink } from 'vue-router'
import HelloWorld from '../components/HelloWorld.vue'

const count = ref(0)
</script>

<style scoped>
/* .v-enter-active,
.v-leave-active {
  transition: all 0.8s ease;
  position: absolute;
  top: -3rem;
  left: -5rem;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
  transform: translateY(3rem);
} */
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
