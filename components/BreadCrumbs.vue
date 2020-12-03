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
                <li v-for="(item, index) in fullSlug" 
                    class="breadCrumb text-gray font-helN font-black capitalize pr-6 relative"
                >
                    <NuxtLink :to="getURL(index)" class="hover:text-white">
                        <template v-if="index == 0">
                            Home
                        </template>
                        <template v-else>
                            {{item.replace(/-/gi, ' ')}}
                        </template>
                    </NuxtLink>
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
        getURL: function(index) {

            switch (index) {
                case 0:  
                    var url = "/";
                    break;
                case this.fullSlug.length - 1: 
                    var url = this.fullSlug.join('/');
                    break;
                default :
                    var url = [] 
                    for (i = 0; i <= index; i++) {
                        url.push(this.fullSlug[i]);
                    }
                    console.log(url);
                    var url = url.join('/');
                    break;
            }

            console.log(this.fullSlug.join('/'));

            return url;
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