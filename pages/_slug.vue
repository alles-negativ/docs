<template>
    <div id="post">
        <h2>{{ post.title }}</h2>
        <nuxt-content :document="post" />
    </div>
</template>

<script>
export default {
    async asyncData({ $content, params, error }) {
        let post;
        try {
            post = await $content("blog", params.slug).fetch();
            // OR const article = await $content(`articles/${params.slug}`).fetch()
        } catch (e) {
            error({ message: "Blog Post not found" });
        }

        return {
            post,
        };
    },
};
</script>

<style>
#post img {
    width: 49.7%;
}
#post p {
    font-size: 20px;
    margin-block-end: 10px;
    margin-block-start: 10px;
}
@media screen and (max-width: 800px) {
    #post img {
        width: 100%;
    }
}
</style>