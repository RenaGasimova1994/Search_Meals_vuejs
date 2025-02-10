<template>
    <div class="max-w-[800px] mx-auto p-8">
  
   <h1 class="text-5xl font-bold mb-5">{{ meal.strMeal }}</h1>
   <img :src="meal.strMealThumb" :alt="meal.strMeal" max-w-100>
   <div class="grid grid-cols-1 sm:grid-cols-3 text-lg py-2">
    <div>
        <strong class="font-bold">Category:</strong> {{ meal.strCategory }}
    </div>
    <div>
        <strong class="font-bold">Area:</strong> {{ meal.strArea }}
    </div>
    <div>
        <strong class="font-bold">Tags:</strong> {{ meal.strTags }}
    </div>
   </div>

    <div class="my-4">{{ meal.strInstructions }}</div>


   <div class="grid grid-cols-1 sm:grid-cols-2 text-lg py-2">
    <div>
        <h2  class="text-2xl mb-3 text-semibold ">Ingredients</h2>
      <ul>
        <template v-for="(ingredient, index) in meal" :key="index">
    <li v-if="meal[`strIngredient${index + 1}`]">
        {{ index + 1 }}. {{ meal[`strIngredient${index + 1}`] }}
    </li>
</template>

      </ul>
     </div>
     <div>
        <h2 class="text-2xl mb-3 text-semibold">Measures</h2>
        <ul>
  <template v-for="(ingredient, index) in Array.from({ length: 20 })" :key="index">
    <li v-if="meal[`strIngredient${index + 1}`]">
        {{ index + 1 }}. {{ meal[`strIngredient${index + 1}`] }}
    </li>
  </template>
</ul>
    </div>
  <div class="my-6"><YoutubeButton :href="meal.strYoutube"> Go to YouTube </YoutubeButton></div>
   <a 
   :href="meal.strSource" 
   target="_blank" 
   class="my-3 px-1 py-3 rounded border-transparent text-center text-white border-2 border-orange-400 bg-yellow-400 hover:bg-yellow-600 bg-text-white transition-colors">
   View Original Source
   </a>
   </div>
    </div>
</template>
<script setup>
import { ref, onMounted} from 'vue';
import { useRoute } from 'vue-router';
import axiosClient from '../axiosClient';
import YoutubeButton from '../components/YoutubeButton.vue';
const route = useRoute()
const meal = ref({})

onMounted(() => {
    axiosClient.get(`lookup.php?i=${route.params.id}`)
        .then((response) => {
            const data = response.data;
            meal.value = data.meals?.[0] || {}; 
        })
        .catch((error) => {
            console.error("Error fetching meal data:", error);
        });
});

</script>