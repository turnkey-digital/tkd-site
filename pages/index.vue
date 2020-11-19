<template>
<div class="bg-black text-white font-helN overflow-hidden">
    <site-header />

    <div class="h-screen w-full z-0 overflow-hidden relative">
        <img v-bind:src="hero.bg" class="absolute w-full left-0 z-0" alt="" />
        <gradient />
        <div class="absolute z-50 w-full flex justify-center bottom-0">
            <div class="container pb-16">
                <div v-html="hero.tagline" class="tagline container mx-auto text-white font-helN text-6xl" />
                <div class="tagline text-white font-prox text-6xl -mt-12"><span>...</span></div>
            </div> 
        </div>
    </div>

    <bio />

    <projects />

    <services />

    <footer-home v-bind="footer"/>

</div>
</template>

<script>
import SiteHeader from "~/components/SiteHeader.vue";
import Gradient from "~/components/home/Gradient.vue";
import Bio from "~/components/home/Bio.vue";
import Projects from "~/components/home/Projects.vue";
import Services from "~/components/home/Services.vue";
import FooterHome from "~/components/home/FooterHome.vue";

export default {
    components: {
        SiteHeader,
        Gradient,
        Bio,
        Projects,
        Services,
        FooterHome,
    },

    mounted() {
        fetch(`${process.env.get_singletons}/home`, {
                headers: {
                    "Cockpit-Token": process.env.token,
                },
            })
            .then((response) => response.json())
            .then((result) => {
                this.hero.bg = process.env.cockpit + result.hero.bg.path;
                this.hero.tagline = result.hero.tagline;
                // this.footer.img = "test";
                
                this.footer.img = process.env.cockpit + result.footImg;
                
                console.log(result);
            });
    },

    data: function () {
        return {
            hero: {
                bg: "",
                tagline: "",
            },
            footer: {
                img: "",
                header: "",
                tagLine: "",
                btn: {
                    text: "",
                    link: ""
                },

            }
        };
    },
};
</script>

<style>
.tagline em {
    font-style: normal;
    color: var(--color-pri);
}
</style>
