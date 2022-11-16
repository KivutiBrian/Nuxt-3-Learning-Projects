<script setup >
    useHead({
        title: "Home - Nuxt3 Concepts",
        meta: [{name:"description", content: "This is Nuxt 3 app demo"}]
    })
</script>


<template>

    <CustomTitle>Home Page</CustomTitle>

    <!-- To lazy load the component -->
    <LazyCustomTitle>Lazy Home Page</LazyCustomTitle>

    <p>This is the index page</p>

    <DashboardStatsCard></DashboardStatsCard>
</template>

