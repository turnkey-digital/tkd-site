<template>
<div>
    <div>
        <img v-bind:src="img" />
    </div>
    <div class="py-24 text-2xl leading-10">
        <div class="container px-8 mx-auto">
            <h3 class="text-5xl mb-4 font-black ">{{header}}</h3>
            <div class="text-xl font-black xl:mr-64 body"  v-html="body" />
        </div>
    </div>
</div>
</template>

<script>

module.exports = {
    props: {
        img: String,
        header: String,
        body: String,
    }
}

</script>

<style>
.body p em {
    font-style: inherit;
    color:var(--color-pri);
}
</style>