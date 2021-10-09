<template lang="">
<header class="header">
    <div class="header__container">
        <img src="../assets/Taggram.svg">
        <div class="current-user">
            <div class="current-user__username" id="current-user-username">{{name}}</div>
            <div class="current-user__avatar" id="current-user-avatar">
                <img v-if="avatar" :src="avatar">
            </div>
        </div>
    </div>
</header>
</template>

<script>
export default {
    props: ["name", "avatar"],
};
</script>

<style lang="" scoped>
.header {
    background-color: #FFF;
    border-bottom: 1px solid #DBDBDB;
}

.header__container {
    display: flex;
    max-width: 950px;
    margin: 0 auto;
    padding: 15px 20px 16px;
}

.current-user {
    margin-left: auto;
    display: flex;
    align-items: center;
}

.current-user__username {
    color: #262626;
    font-family: Arial, sans-serif;
    font-size: 14px;
    line-height: 18px;
    margin-right: 12px;
}

.current-user__avatar {
    height: 28px;
    width: 28px;
    background-color: #DBDBDB;
    border-radius: 50%;
    background-repeat: no-repeat;
    background-size: contain;
    overflow: hidden;
}

.current-user img {
    max-height: 100%;
    max-width: 100%;
    object-fit: cover;
}
</style>
