<template>
<div class="comment">
    <div>
        <div class="avatar">
            <img v-if="info.user.avatar" :src="info.user.avatar" alt="">
        </div>
    </div>
    <div class="center">
        <b>{{info.user.username}}</b> {{info.message}}
        <div class="bottom">
            <div class="time">{{getPassedTime(info.created_at)}}</div>
            <div class="likes">{{info.like_count > 0 ? info.like_count > 1 ? `${info.like_count} curtidas` : `${info.like_count} curtida` : ""}}</div>
        </div>
    </div>
    <div class="fav">
        <img v-if="info.has_liked" src="../assets/liked.svg" v-on:click="unlike(info.uuid)">
        <img v-else src="../assets/not_liked.svg" v-on:click="like(info.uuid)">
    </div>
    <alert v-if="erro.occured" :text="erro.message" :duration="erro.duration" v-on:close="erro.occured = false"></alert>
</div>
</template>

<script>
import Alert from "./alert-modal.vue";

export default {
    components: {
        "alert": Alert,
    },
    props: ["info", "current_user"],
    data() {
        return {
            erro: {}
        }
    },
    methods: {
        getPassedTime(since) {
            var passedTime = new Date() - new Date(since);

            passedTime /= 1000;

            var seconds = Math.round(passedTime);
            var minutes = Math.round(seconds / 60);
            var hours = Math.round(minutes / 60);

            if (hours > 0)
                return `${hours}h`;

            if (minutes > 0)
                return `${minutes}min`;

            return `${seconds}sec`;
        },
        like(uuid) {
            this.$http.post(`https://taggram.herokuapp.com/comments/${uuid}/like`, {
                    "username": this.current_user
                })
                .then(res => res.json())
                .then(data => this.$emit("update", data))
                .catch(err =>
                    this.erro = {
                        occured: true,
                        message: "Erro ao curtir comentário!",
                        duration: 2
                    }
                );
        },
        unlike(uuid) {
            this.$http.post(`https://taggram.herokuapp.com/comments/${uuid}/unlike`, {
                    "username": this.current_user
                })
                .then(res => res.json())
                .then(data => this.$emit("update", data))
                .catch(err =>
                    this.erro = {
                        occured: true,
                        message: "Erro ao descurtir comentário!",
                        duration: 2
                    });
        }
    },
}
</script>

<style scoped>
.comment {
    padding: 18px 22px;
    display: flex;
    column-gap: 18px;
}

.center {
    flex: 1;
}

.bottom {
    display: flex;
    column-gap: 10px;
    padding-top: 18px;
    font-size: 15px;
}

.time {
    color: #8E8E8E;
}

.likes {
    color: #8E8E8E;
    font-weight: bold;
}

.avatar {
    height: 35px;
    width: 35px;
    background-color: #DBDBDB;
    border-radius: 50%;
    overflow: hidden;
}

.avatar img {
    width: 100%;
    background: #DBDBDB !important;
    object-fit: cover;
}

.fav {
    font-size: 15px;
}

.fav img {
    height: 1em;
    cursor: pointer;
}
</style>
