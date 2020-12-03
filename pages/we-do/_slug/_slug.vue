<template>
    <div class="bg-black text-white font-helN overflow-hidden">

        <site-header  />
        <bread-crumbs  />

        {{$route.path}}

        <bio v-bind="bioHTML" />


        <Footer />
        
    </div>
</template>

<script>
import WeDoFooter from "~/components/we-do/Footer.vue";

import SiteHeader from "~/components/SiteHeader.vue";
import BreadCrumbs from "~/components/BreadCrumbs.vue";
import Bio from "~/components/Bio.vue";
import Services from "~/components/Services.vue";
import Footer from "~/components/Footer.vue";

export default {
    components: {
        WeDoFooter,
        
        SiteHeader,
        BreadCrumbs,
        Bio,
        Services,
        Footer,
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
            
                this.weDoFooter.img = process.env.cockpit + result.footer.img.path
                this.weDoFooter.header = result.footer.header
                this.weDoFooter.body = result.footer.body

            });
    },

    data: function () {
        return {
            title:"",
            bioHTML: {
                html:"<h1><em>We do</em>. We work hard. We have good ideas. We figure it out. We ask questions. We are honest. We love what we do. We shake things up. We explore. We deliver.</h1>",
            },
            weDoFooter: {
                img:"https://cockpit.server9.turnkeydigital.dev/storage/uploads/2020/11/30/5fc51e2859733we-do-footer.jpg",
                header:"Our Process text, or Are we a good fit text?",
                body:"<p><em>Good question.</em> Because we’re passionate and committed about what we do, that dedication is reflected in every single project we take on. We work hard for your business—as if it were our own, and we want you to succeed. To do that we need cooperation, honest communication, and to essentially form a partnership...Our capabilities may not be in line with exactly what you need, in which case, we will always be honest with you about that, and furthermore, suggest what might be a better path for your business.</p>"
            }
        };
    },
};
</script>