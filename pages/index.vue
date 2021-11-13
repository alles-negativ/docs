<template>
    <div id="content">
        <div class="post" v-for="post of posts" :key="post.slug">
            <NuxtLink :to="'/' + post.slug">{{ post.project.toUpperCase() + ": " + post.title + " / " + $moment(post.date).format("DD.MM.YYYY") }}</NuxtLink>
        </div>
    </div>
</template>

<script>
export default {
    async asyncData({ $content }) {
        const posts = await $content("blog").sortBy('date', 'desc').fetch();

        return {
            posts,
        };
    },
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
</style>