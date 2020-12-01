<template>
<div class="z-50 w-full flex justify-center bottom-0">
    <div class="container px-24 py-24 text-2xl leading-10 masonary">
        <div v-if="loadingCats">
            <h6>Loading..</h6>
        </div>
        <div v-else v-for="serviceCategory in serviceCategories"  class="mb-16 serviceCategory">
            <h2 class="text-6xl font-black font-helN">{{serviceCategory.title}}</h2>
            
            <span v-if="loadingServices">Loading...</span>
            
            <ul v-else class="mt-4 ledding-4 services">
                <template v-for="service in services">
                    <li v-if="service.category._id == serviceCategory._id" :key="service._id" class="text-gray hover:text-pri font-helN"><a v-bind:href="fixURL(serviceCategory.title, service.title)">{{service.title}}</a></li>
                </template>
            </ul>
        </div>
    </div>
</div>
</template>

<script>

module.exports = {
     mounted() {
        fetch(`${process.env.get_serviceCategories}&sort[order]=1`)
            .then(response => response.json())
            .then(result => {
                this.serviceCategories = result.entries
                this.loadingCats = false;
            }),
        fetch(`${process.env.get_services}`)
            .then(response => response.json())
            .then(result => {
                console.group('Services')
                    console.log(result.entries)
                console.groupEnd()

                this.services = result.entries
                this.loadingServices = false;
            })
    },

    methods:  {
        fixURL: function(cat, page) {
            cat = cat.replace(/[^a-z0-9]/gi, '-').toLowerCase().replace(/---/gi, '-');
            page = page.replace(/[^a-z0-9]/gi, '-').toLowerCase().replace(/---/gi, '-');

            var url = 'we-do/' + cat + '/' + page;

            return url;
        }
    },

    data: function() {
        return {
            loadingCats: true,
            loadingServices: true,
            serviceCategories: Array,
            services: Array
        }
    }
}

</script>

<style scoped>
    .masonary {
        column-gap: 1.5em;
        column-count: 2;
    }
    .serviceCategory {
        display: inline-block;
        width: 100%;
    }
    .services li {
        transition:300ms;
    }
    .services li:hover {
        padding-left:1em;
    }
</style>