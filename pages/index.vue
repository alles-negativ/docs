<template>
    <div id="content">
        <div class="categories">
            <p v-for="categorie of categories" :key="categorie.id" @click="getSelection(categorie, $event)">
                {{ categorie }}
            </p>
        </div>
        <div class="post" v-for="post of posts" :key="post.id">
            <NuxtLink :to="'/' + post.slug">{{ post.project.toUpperCase() + ": " + post.title + " / " + $moment(post.date).format("DD.MM.YYYY") }}</NuxtLink>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            categories: []
        }
    },
    async asyncData({ $content }) {
        const posts = await $content("blog").sortBy('date', 'desc').fetch();
        // const posts = await $content("blog").where({ project: 'streamline' }).sortBy('date', 'desc').fetch();
        return {
            posts,
        };
    },
    methods: {
        setCategories: function (event) {
            var output = ["all"]
            this.posts.forEach(post => {
                if (!output.includes(post.project)) {
                    output.push(post.project)
                }
            });
            this.categories = output
        },
        getSelection: async function(categorie, event) {
            document.querySelectorAll(".categories p").forEach(element => {
                element.classList.remove("active")
            });
            event.target.className = "active"
            if (categorie != "all") {
                this.posts = await this.$content("blog").where({ project: categorie }).sortBy('date', 'desc').fetch();
            } else {
                this.posts = await this.$content("blog").sortBy('date', 'desc').fetch();
            }
        }
    },
    mounted() {
        this.setCategories()
    }
};
</script>

<style>
#content {
    display: flex;
    flex-flow: row wrap;
    width: 100%;
    margin-top: 10px;
}
.post {
    display: flex;
    background: #8a2be266;
    margin: 0 10px 10px 0;
}
.post:hover {
    display: flex;
    background: blueviolet;
    margin: 0 10px 10px 0;
}
.post a {
    color: black;
    text-decoration: none;
    padding: 10px;
}
.post a:hover {
    color: white;
}
.categories {
    width: 100%;
}
.categories p {
    display: inline-block;
    margin: 0 10px 10px 0;
}
.categories p:hover {
    /* color: blueviolet; */
    text-decoration: underline;
}
.categories p.active {
    color: blueviolet;
}
</style>