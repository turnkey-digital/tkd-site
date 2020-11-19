<template>
<div class="z-50 w-full flex justify-center bottom-0">
    <div class="container py-24 text-2xl leading-10 grid grid-cols-2">
        <h1>Testing</h1>
        {{img}}
    </div>
</div>
</template>

<script>

module.exports = {
    props: {
        img: String,
        header: String,
        tagLine: String,
        btnTxt: String,
        btnLink: String,
    }
    
}

</script>