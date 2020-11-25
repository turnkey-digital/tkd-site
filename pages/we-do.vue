<template>
    <div>

        <site-header class="bg-black" />
        <bread-crumbs class="bg-black" />

        <bio v-bind="bioHTML" class="bg-black" />
        
    </div>
</template>

<script>
import SiteHeader from "~/components/SiteHeader.vue";
import BreadCrumbs from "~/components/BreadCrumbs.vue";
import Bio from "~/components/Bio.vue";

export default {
    components: {
        SiteHeader,
        BreadCrumbs,
        Bio,
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

                this.title = result.title
                this.bioHTML.html = result.bio
            
            });
    },

    data: function () {
        return {
            title:"",
            bioHTML: {
                html:"",
            }
        };
    },
};
</script>