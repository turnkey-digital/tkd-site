<template>
<div class="bg-black text-white font-helN overflow-hidden">
    <site-header class="absolute" />

    <home-hero v-bind="hero" />

    <home-bio />

    <home-projects />

    <services />

    <home-footer v-bind="footer"/>

</div>
</template>

<script>
import HomeHero from "~/components/home/HomeHero.vue";
import HomeBio from "~/components/home/HomeBio.vue";
import HomeProjects from "~/components/home/HomeProjects.vue";
import HomeFooter from "~/components/home/HomeFooter.vue";

import SiteHeader from "~/components/SiteHeader.vue";
import Services from "~/components/Services.vue";

export default {
    components: {
        HomeHero,
        HomeBio,
        HomeProjects,
        HomeFooter,

        SiteHeader,
        Services,
    },

    mounted() {
        fetch(`${process.env.get_singletons}/home`, {
                headers: {
                    "Cockpit-Token": process.env.token,
                },
            })
            .then((response) => response.json())
            .then((result) => {
                this.hero.bg = result.hero.bg;
                this.hero.tagline = result.hero.tagline;

                console.log(result)
                
                this.footer.img = process.env.cockpit + result.footerImg.path;
                this.footer.header = result.footerHeader;
                this.footer.tagLine = result.footerTagline;
                this.footer.btnTxt = result.footerBtnTxt;
                this.footer.btnLink = result.footerBtnLink;
                this.footer.copyRight = result.copyRight;

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
                btnTxt:"",
                btnLink:"",
                copyRight:""
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
