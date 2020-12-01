<template>
    <div class="projects_parent grid grid-cols-3 xl:grid-cols-5">
        <div v-if="loading">
            <h6>Loading...</h6>
        </div>
        <NuxtLink v-for="project in projects" :key="project._id" :to="'our-work/' + project.projectTitle.replace(/[^a-z0-9]/gi, '-').toLowerCase().replace(/---/gi, '-')" class="project">
            <span>
                <div class="shapeshifter play" style="background-image: url('https://cockpit.server9.turnkeydigital.dev/storage/uploads/2020/11/30/5fc5583d551bcsprite_60fps.svg')"></div>
            </span>
            <img v-bind:src="imageURL + project.homeImage.path" /> 
        </NuxtLink>
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

<style scoped>
    .projects_parent:hover .project {
        opacity:.5;
    }
    .project {
        position:relative;
        overflow:hidden;
        transition:var(--trans-fast);
    }
    .projects_parent:hover .project:hover {
        z-index:2;
        transform:scale(1.1);
        border-radius:.3em;
        box-shadow:0px 5px 10px rgba(0,0,0,.5);
        opacity:1;
    }
    .project span {
        width:3em;
        height:3em;
        position:absolute;
        right:0em;
        bottom:0em;
        z-index:10;
    }

    .project:after {
        content:" ";
        position:absolute;
        height:100%;
        width:100%;
        background:black;
        top:0;
        z-index:1;
        opacity:0;
        transition:var(--trans-fast);
    }
    .project:hover:after {
    }

    .shapeshifter {
        width: 24px;
        height: 24px;
        background-repeat: no-repeat;
        background-position: 0px 0px;
        transition:var(--trans-fast) steps(18);
    }
    .project:hover .shapeshifter {
        background-position: -432px 0px;
    }

    @media(max-width:1280px) {
        .projects_parent div:nth-of-type(10) {
            display:none;
        }
    }
</style>