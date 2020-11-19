<template>
    <div class="grid grid-cols-3 xl:grid-cols-5">
        <div v-if="loading">
            <h6>Loading...</h6>
        </div>
        <div v-for="project in projects" :key="project._id">
            <img v-bind:src="imageURL + project.homeImage.path" /> 
        </div>
    </div>
</template>

<script>

module.exports = {
     mounted() {
        fetch(`${process.env.get_projects}&filter[featuredHome]=true&sort[homeOrder]=1`)
            .then(response => response.json())
            .then(result => {
                console.log(result.entries);

                this.projects = result.entries;
                this.loading = false;
            })
    },

    data: function() {
        return {
            loading: true,
            projects: Array,
            imageURL: process.env.cockpit
        }
    }
}

</script>