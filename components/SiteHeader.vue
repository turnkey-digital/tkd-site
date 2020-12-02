<template>
<div class="z-50 w-full flex justify-center">
    <div class="container px-8 flex justify-center py-8 z-50 ">
        <!-- Loading State --> 
        
        <div v-if="loading" class="w-full text-center">
            <div class="w-full flex justify-between content-end">
                <a href="/" class="block w-48">
                    <img src="https://cockpit.server9.turnkeydigital.dev/storage/uploads/2020/09/28/5f7243d2e5729new_tkd_logo.svg" alt="">
                </a>
                <ul class="flex justify-between content-end">
                    <li class="font-helN font-black ml-4 uppercase text-gray transition duration-500 hover:text-pri self-end">
                        <a href="we-do" class="self-end">We Do</a>
                    </li>
                    <li class="font-helN font-black ml-4 uppercase text-gray transition duration-500 hover:text-pri self-end">
                        <a href="our-work" class="self-end">Our Work</a>
                    </li>
                    <li class="font-helN font-black ml-4 uppercase text-gray transition duration-500 hover:text-pri self-end">
                        <a href="about-turnkey-digital" class="self-end">About</a>
                    </li>
                    <li class="font-helN font-black ml-4 uppercase text-gray transition duration-500 hover:text-pri self-end">
                        <a href="contact" class="self-end">Contact</a>
                    </li>
                </ul>
            </div>
        </div>

        <!-- Live State --> 
        <div v-else class="w-full flex justify-between content-end">
            <a href="/" class="block w-48">
                <img :src="siteHeader.logo" alt="">
            </a>
            <ul class="flex justify-between content-end">
                <li v-for="nav in siteHeader.navigation" :key="nav.__ob__.dep.id" class="font-helN font-black ml-4 uppercase text-gray transition duration-500 hover:text-pri self-end">
                    <NuxtLink :to="'../'+nav.value.url" 
                        :prefetch="false"
                        :class="{ 'text-pri': $route.params.slug === nav.value.url }"
                        class="self-end"
                    >
                            {{nav.value.title}}
                    </NuxtLink>
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
                // console.log(result.navigation);
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
