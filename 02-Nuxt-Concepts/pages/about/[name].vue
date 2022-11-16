<script setup>

const route = useRoute()

</script>

<template>
    <div>
        THis is all about {{route.params.name}}
    </div>
</template>