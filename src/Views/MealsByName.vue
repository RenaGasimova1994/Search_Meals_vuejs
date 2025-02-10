<template>
  <div class="p-8 pb-0">
    <input 
    v-model="keyword"
    type="text" 
    class="rounded border-2 border-gray200 w-full mb-5" 
    placeholder="Search for meals"
    @input="searchMeals">
  </div>

  <div v-if="!meals.length" class="text-center text-gray-600 p-4">
    No meals found. Please try a different keyword.
  </div>

 <Meals v-else :meals="meals" />

</template>
    <script setup>
     import { computed, onMounted, ref } from 'vue';
     import store from '../store';
     import { useRoute } from 'vue-router';
     import Meals from '../components/Meals.vue';

     const route = useRoute();
     const keyword = ref('')
     const meals = computed(()=>store.state.searchedMeals)
     function searchMeals() {
       
    if (keyword.value.trim()) { 

        store.dispatch('searchMeals', keyword.value.trim());
    } else {
        store.commit('setSearchedMeals', []);  
    }}

     onMounted(() => {
        keyword.value = route.params.name
        if(keyword.value){
            searchMeals() 
        }
     })

</script>
    <style>
</style>