<template>
<div class="z-50 w-full flex justify-center bottom-0">
    <div class="container py-24 text-2xl leading-10">
        <div v-if="loading">
            <h6>Loading...</h6>
        </div>
        <div v-else v-html="bio" />
    </div>
</div>
</template>

<script>

module.exports = {
     mounted() {
        fetch(`${process.env.get_singletons}/home`, {
                headers: {
                    'Cockpit-Token': process.env.token
                }
            })
            .then(response => response.json())
            .then(result => {
                this.bio = result.bio
                this.loading = false;
            })
    },

    data: function() {
        return {
            loading: true,
            bio: String
        }
    }
}

</script>