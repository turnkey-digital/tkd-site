<template>
    <div class="h-screen w-full z-0 overflow-hidden relative">
        <video v-bind:src="bg" class="absolute left-1_2 min-w-full min-h-full max-w-none z-0 transform -translate-x-1/2" autoplay loop />
        
        <gradient />

        <div class="absolute z-50 w-full flex justify-center bottom-0">
            <div class="container px-8 pb-16">
                <div v-html="tagline" class="tagline mx-auto text-white font-helN text-6xl" />
                <div class="tagline text-white font-prox text-6xl -mt-12"><span>...</span></div>
            </div> 
        </div>
    </div>
</template>

<script>

import Gradient from "~/components/home/Gradient.vue";

export default {
    components: {
        Gradient
    },
    
    props: {
        bg: String,
        tagline: String,
    }

}

// module.exports = {
// }

</script>

<style scoped>
    .left-1_2 {
        left:50%;
    }
</style>

