<template lang="">
    <img :src="post.photo"> </img>
</template>

<script>
export default {
    props: ["post"],
}
</script>

<style lang="" scoped>
    img {
        object-fit: scale-down;
        width: 100%;
    }
    
</style>