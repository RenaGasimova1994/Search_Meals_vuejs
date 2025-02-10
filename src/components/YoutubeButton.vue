<template>
   <a 
   :href="href" 
   target="_blank" 
   class="px-4 py-4 rounded text-white border-2 border-red-600 bg-red-400 hover:bg-red-600 bg-text-white transition-colors">
   <slot>Youtube</slot>
   </a>
</template>
<script setup>

const props = defineProps({
    href: {type: String,
    required: true},
})


</script>