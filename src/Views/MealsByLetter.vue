<template>
    <div class="flex justify-center mt-2 gap-2"> 
     <router-link 
     :to="{name: 'byLetter', params: {letter}}" 
     v-for="letter in letters"  
     :key="letter"> {{ letter }}
    </router-link>
    </div>
    
    <Meals :meals="meals" />
   
   </template>
    <script setup>
    import { onMounted, watch } from 'vue';
    import { useRoute } from 'vue-router';
    import { computed } from 'vue';
    import store from '../store';
    import Meals from '../components/Meals.vue';




    const letters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'.split("");
    const meals = computed(() => store.state.mealsByLetter);
    const route = useRoute();
    
    function fetchMealsByLetter(letter) {
      console.log("Fetching meals for:", letter);
      store.dispatch('searchMealsByLetter', letter);
    }
    
    onMounted(() => {
      fetchMealsByLetter(route.params.letter);
    });
    
    watch(() => route.params.letter, (newLetter) => {
      fetchMealsByLetter(newLetter);
    });
    
    watch(() => route.name, () => {

  store.dispatch('resetMealsByLetter'); 
    });
   </script>

   <style></style>


