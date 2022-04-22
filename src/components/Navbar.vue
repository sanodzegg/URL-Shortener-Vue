<script setup>
    import Burger from './Burger.vue'
</script>

<script>
  export default {
    data() {
      return {
        displayBurger: false,
      }
    }
  }
</script>

<template>
  <nav class="navbar">
      <div class="navbar__l">
        <h1 class="navbar__logo">Shortly</h1>
        <ul class="navbar__navigation">
            <li>Features</li>
            <li>Pricing</li>
            <li>Resources</li>
        </ul>
      </div>
      <div class="navbar__r">
          <button class="navbar__login">Login</button>
          <button class="navbar__signup">Sign Up</button>
          <div class="burger__menu" v-on:click="displayBurger = !displayBurger">
            <div class="shape"></div>
            <div class="shape"></div>
            <div class="shape"></div>
          </div>
      </div>
  </nav>
  <div class="burger__menu__display" v-if="displayBurger">
    <Burger />
  </div>
</template>