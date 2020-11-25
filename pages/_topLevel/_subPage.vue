<template>
    <div>

        <site-header class="bg-black" />
        <bread-crumbs class="bg-black" />

        <h1>{{ $route.path }}</h1>
        <h1>{{ title }}</h1>
    </div>
</template>

<script>
import SiteHeader from "~/components/SiteHeader.vue";
import BreadCrumbs from "~/components/BreadCrumbs.vue";

export default {
    components: {
        SiteHeader,
        BreadCrumbs,
    },

    mounted() {
        // console.log(this.$route.params.slug.replace(/-/gi, ''));

        fetch(`${process.env.get_singletons}${this.$route.path.replace(/-/gi, '')}`, {
                headers: {
                    "Cockpit-Token": process.env.token,
                },
            })
            .then((response) => response.json())
            .then((result) => {

                console.log(result)

                // this.title = result.title
            
            });
    },

    data: function () {
        return {
            title:"",
        };
    },
};
</script>