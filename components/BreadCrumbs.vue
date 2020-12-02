<template>
<div class="z-50 w-full flex justify-center">
    <div class="container px-8 pb-8 flex justify-center  z-50 ">
        <!-- Loading State --> 
        
        <div v-if="loading" class="w-full">
            <span class="text-pri">Loading</span>
        </div>

        <!-- Live State --> 
        <div v-else class="w-full flex justify-between content-end">
            <ul class="flex">
                <li class="text-gray font-helN font-black hover:text-pri">
                    <NuxtLink to="/">Home</NuxtLink>
                </li>
                <li v-for="(item, index) in fullSlug" 
                    class="text-gray font-helN font-black capitalize pr-6 relative breadCrumb"
                >
                    <NuxtLink :to="'../'+item">{{ index }}, {{ item }} | {{getURL(index)}}</NuxtLink>
                </li>
                
            </ul>
        </div>
    </div>
</div>
</template>

<script>
module.exports = {
    data: function() {
        return {
            fullSlug: this.$route.fullPath.split('/'),
        }
    },
    methods:  {
        getURL: function() {
            console.log("Whitey's on the moon " + index);
        }
    }
    // mounted() {
    //     console.log(this.$route.fullPath);

    //     this.loading:false;
    //     this.route:
    // },

    // data: function () {
    //     return {
    //         loading: true,
    //         route: String
    //     }
    // }
}
</script>

<style scoped>
.breadCrumb:after {
    content:":";
    position:absolute;
    right:.75rem;
}
.breadCrumb:nth-last-of-type(1):after {
    content:'';
}
</style>