<script setup>
import Navbar from './components/Navbar.vue'
import MainSection from './components/MainSection.vue'
import BeforeFooter from './components/BeforeFooter.vue';
import Footer from './components/Footer.vue';
</script>

<template>
      <main>
            <Navbar />
            <MainSection />
            <BeforeFooter />
            <Footer />
      </main>
</template>

<style>
@import url("../src/assets/master.css");
</style>
