<template>
<div class="absolute z-50 w-full flex justify-center">
    <div class="container flex justify-center py-8 z-50 ">
        <div v-if="loading" class="w-full text-center">
            <span class="font-mono font-bold text-white text-opacity-50">Header is loading....</span>
        </div>
        <div v-else class="w-full flex justify-between content-end">
            <a href="/" class="block w-48">
                <img :src="siteHeader.logo" alt="">
            </a>
            <ul class="flex justify-between content-end">
                <li v-for="nav in siteHeader.navigation" :key="nav.__ob__.dep.id" class="font-helN font-black ml-4 uppercase text-gray transition duration-500 hover:text-pri self-end">
                    <a :href="nav.value.url" class="self-end">
                        {{nav.value.title}}
                    </a>
                </li>
            </ul>
        </div>
    </div>
</div>
</template>

<script>
module.exports = {
    mounted() {
        fetch(`${process.env.get_singletons}/siteHeader`, {
                headers: {
                    'Cockpit-Token': process.env.token
                }
            })
            .then(response => response.json())
            .then(result => {
                // console.log(result);
                this.siteHeader.logo = process.env.cockpit + result.logo.path;
                this.siteHeader.navigation = result.navigation;
                this.loading = false;
            })
    },

    data: function () {
        return {
            loading: true,
            siteHeader: {
                logo: null,
                navigation: []
            }
        }
    }
}
</script>
