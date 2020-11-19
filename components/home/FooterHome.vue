<template>
<div>
    <div>
        <img v-bind:src="img" />
    </div>
    <div class="bg-pri py-24 text-2xl leading-10">
        <div class="container mx-auto">
            <h3 class="text-4xl text-black font-black font-helN">{{header}}</h3>
            <h4 class="text-xl text-black font-black font-helN">{{tagLine}}</h4>
            <button class="mx-auto border block px-4 py-2 mt-8 leading-none text-base text-black font-helN">{{btnTxt}}</button>
        </div>
    </div>
    <div v-if="isActive" class="container mx-auto py-4">
        <h1>Hello World!</h1>
    </div>
    <div class="container mx-auto py-4 flex justify-between">
        <p>HEllo</p>
        <button v-on:click="myFilter" v-bind:class="{ 'is-active': isActive }" class="hamburger hamburger--squeeze" type="button">
            <span class="hamburger-box">
                <span class="hamburger-inner"></span>
            </span>
        </button>
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
    },

    data: function() {
        return {
            isActive: false,
        }
    },

    methods: {
        myFilter: function() {
        this.isActive = !this.isActive;
        // some code to filter users
        }
    }
    
}

</script>

<style scoped>
.hamburger-inner, .hamburger-inner::after, .hamburger-inner::before,
.hamburger.is-active .hamburger-inner, .hamburger.is-active .hamburger-inner::after, .hamburger.is-active .hamburger-inner::before {
    background:white;
}

button.hamburger.hamburger--squeeze {
    padding: 0;
}

span.hamburger-inner {
    width: 75%;
    transform: rotate(180deg);
    right: 0;
}
.is-active span.hamburger-inner {
    width: 100%;
    transform: rotate(45deg);
    right: unset;
}
</style>