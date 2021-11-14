<template>
    <div id="header">
        <h1>
            alles-negativ/<NuxtLink to="/">Docs</NuxtLink>
        </h1>
    </div>
</template>

<style>
#header {
    /* border-bottom: solid 2px; */
}
#header h1 {
    font-style: italic;
    text-decoration: none;
    margin-top: 5px;
}
#header a {
    color: blueviolet;
    text-decoration: none;
}
#header a:hover {
    text-decoration: underline;
}
#header a.nuxt-link-exact-active {
    text-decoration: underline;
}
</style>