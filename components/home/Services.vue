<template>
<div class="z-50 w-full flex justify-center bottom-0">
    <div class="container py-24 text-2xl leading-10 grid grid-cols-2">
        <div v-if="loadingCats">
            <h6>Loading..</h6>
        </div>
        <div v-else v-for="serviceCategory in serviceCategories"  class="mb-16">
            <h2 class="text-6xl">{{serviceCategory.title}}</h2>
            
            <span v-if="loadingServices">Loading...</span>
            
            <ul v-else>
                <template v-for="service in services">
                    <li v-if="service.category._id == serviceCategory._id" :key="service._id">
                        {{service.title}}
                    </li>
                </template>
            </ul>
        </div>
    </div>
</div>
</template>

<script>

module.exports = {
     mounted() {
        fetch(`${process.env.get_serviceCategories}`)
            .then(response => response.json())
            .then(result => {
                console.group('Services Cats')
                    console.log(result.entries)
                console.groupEnd()

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