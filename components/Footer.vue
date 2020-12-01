<template>
<div>
    <div class="bg-pri py-24 text-2xl leading-10">
        <div class="container px-8 mx-auto">
            <h3 class="text-4xl text-black font-black font-helN">{{header}}</h3>
            <h4 class="text-xl text-black font-black font-helN" v-html="tagline"></h4>
        </div>
    </div>
    <div>
        <div v-bind:class="{ 'is-show': isActive }" class="footerModal block h-screen w-screen bg-black">
            <div class="container mx-auto py-24"  v-html="modal" />
        </div>
        <div class="container px-8 mx-auto py-4 flex justify-between ">
            <p class="z-10">{{copyRight}}</p>
            <button v-on:click="myFilter" v-bind:class="{ 'is-active': isActive }" class="hamburger hamburger--squeeze" type="button">
                <span class="hamburger-box">
                    <span class="hamburger-inner"></span>
                </span>
            </button>
        </div>
    </div>
</div>
</template>

<script>

module.exports = {
    mounted() {
        fetch(`${process.env.get_singletons}/footer`, {
                headers: {
                    "Cockpit-Token": process.env.token,
                },
            })
            .then((response) => response.json())
            .then((result) => {

                console.log(result)

                this.tagline = result.tagline
                this.copyRight = result.copyRight
                this.modal = result.modal

            });
    },

    data: function() {
        return {
            isActive: false, 
            tagline: "",
            copyRight: "",
            modal: "",
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

.footerModal {
    opacity:0;
    position:fixed;
    bottom:-100%;
    transition:500ms;
}
.footerModal.is-show {
    opacity:1;
    bottom:0%;
}
</style>