<template>
<div class="bg-black text-white font-helN overflow-hidden">
    <site-header />

    <home-hero v-bind="hero" />

    <bio />

    <projects />

    <services />

    <footer-home v-bind="footer"/>

</div>
</template>

<script>
import HomeHero from "~/components/home/HomeHero.vue";
import Bio from "~/components/home/Bio.vue";
import Projects from "~/components/home/Projects.vue";
import FooterHome from "~/components/home/FooterHome.vue";

import SiteHeader from "~/components/SiteHeader.vue";
import Services from "~/components/Services.vue";

export default {
    components: {
        SiteHeader,
        HomeHero,
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
                
                this.footer.img = process.env.cockpit + result.footerImg.path;
                this.footer.header = result.footerHeader;
                this.footer.tagLine = result.footerTagline;
                this.footer.btnTxt = result.footerBtnTxt;
                this.footer.btnLink =result.footerBtnLink;

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
                btnLink:""
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
