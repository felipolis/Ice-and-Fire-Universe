<script setup>
  import { ref } from 'vue'
  import Hero from '../components/Hero.vue';
  import ShowCards from '../components/ShowCards.vue';
  import BookCards from '../components/BookCards.vue';
  


  const isShow = ref(true);
</script>


<template>
  <main>

    <Hero 
      :isShow="isShow"
      @selectPlatform="isShow = !isShow"
    />

    <keep-alive>
      <component :is="isShow ? ShowCards : BookCards"></component>
    </keep-alive>

  </main>
</template>
