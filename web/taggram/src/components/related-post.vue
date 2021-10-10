<template>
    <img :src="image">
</template>

<script>
export default {
    props: ["image"],
}
</script>

<style scoped>
img {
    object-fit: scale-down;
    width: 100%;
}
</style>
