<template>
<div class="z-50 w-full flex justify-center bottom-0 z-10">
    <div class="container px-8 py-24 text-2xl leading-10">
        <div class="bio mx-auto text-white font-helN text-6xl font-black" v-html="html" />
        <div class="bio text-white font-helN text-6xl -mt-8"><span>...</span></div>
    </div>
</div>
</template>

<script>

module.exports = {
     props: {
        html: String,
    },

}

</script>

<style>
.bio {
    line-height:5rem;
}
.bio em {
    font-style: normal;
    color: var(--color-pri);
}
</style>