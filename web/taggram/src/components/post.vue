<template>
<div id="container">
    <div class="photo">
        <img :src="post.photo" alt="" srcset="">
    </div>
    <div class="post_right">
        <div class="post_user">
            <div class="user_avatar">
                <div class="avatar">
                    <img v-if="post.user.avatar" :src="post.user.avatar" alt="">
                </div>
            </div>
            <div class="user_infos">
                <div class="user_name"> {{post.user.username}}</div>
                <div class="user_locale">{{post.location.city}}, {{post.location.country}}</div>
            </div>
        </div>
        <div class="post_comments">
            <post-comment v-for="(comment, i) of post.comments" :info="comment" :current_user="post.user.username" :key="i" v-on:update="post.comments[i] = $event, $forceUpdate()"> </post-comment>
        </div>
        <div class="post_infos">
            <div class="post_comment_count">{{post.comments.length == 1 ? `${post.comments.length} comentário` : `${post.comments.length} comentários`}} </div>
            <div class="post_date">{{post.created_at}}</div>
        </div>
    </div>
</div>
</template>

<script>
import Comment from "./comment-post.vue";

export default {
    props: ["post"],
    components: {
        "post-comment": Comment,
    },
}
</script>

<style scoped>
#container {
    border-radius: 3px;
    border: 1px solid #DBDBDB;
    overflow: hidden;
    display: grid;
    grid-template-columns: 8fr 5fr;
}

.photo img {
    width: 100%;
    height: 100%;
}

.post_right {
    background: #FFF;
    display: flex;
    flex-direction: column;
}

::-webkit-scrollbar {
    width: 0px;
}

.post_user {
    display: flex;
    padding: 20px 22px;
    border-bottom: 1px solid #EFEFEF;
}

.user_infos {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    padding-left: 15px;
}

.user_name {
    font-style: normal;
    font-weight: bold;
    font-family: arial;
}

.avatar {
    overflow: hidden;
    height: 35px;
    width: 35px;
    border-radius: 50%;
    background-color: #DBDBDB;
}

.user_avatar img {
  width: 100%;
  height: 100%;
  background: #DBDBDB !important;
  object-fit: cover;
}

.user_locale {
    font-size: 13px;
}

.post_comments {
    flex: 1;
    max-height: 410px;
    overflow-y: scroll;
    padding-bottom: 20px;
}

.post_infos {
    border-top: 1px solid #EFEFEF;
    padding: 20px 18px 12px;
}

.post_comment_count {
    color: #262626;
    font-weight: 750;
}

.post_date {
    color: #8E8E8E;
    font-size: 13px;
    line-height: 30px;
}
</style>
