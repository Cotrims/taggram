<template>
<div id="app">
    <top-header :name="currentUser.username" :avatar="currentUser.avatar"></top-header>
    <div id="content">
        <post :post="post"></post>
        <hr>
        <p>Mais publicações</p>
        <div class="related-posts">
            <div id="related" v-for="(rel, i) of relateds" :key="i">
                <related-post :post="rel"></related-post>
            </div>
        </div>
    </div>
    <footer>
        <img src="./assets/tagview.svg" alt="">
    </footer>
</div>
</template>

<script>
import Header from "./components/header.vue";
import Related from "./components/related-post.vue";
import Post from "./components/post.vue";

export default {
    name: 'app',
    components: {
        "top-header": Header,
        "related-post": Related,
        "post": Post
    },
    data() {
        return {
            currentUser: {},
            post: {},
            relateds: [],
        }
    },
    methods: {
        getUser() {
            this.$http.get('https://taggram.herokuapp.com/me')
                .then(res => res.json())
                .then(data => (this.currentUser = data, this.getPost()))
                .catch(err => console.log(err));
        },
        getPost() {
            this.$http.get('https://taggram.herokuapp.com/post', {
                    params: {
                        username: this.currentUser.username
                    }
                })
                .then(res => res.json())
                .then(data => (this.post = data, this.getRelateds()))
                .catch(err => console.log(err));
        },
        getRelateds() {
            this.$http.get(`https://taggram.herokuapp.com/posts/${this.post.uuid}/related`)
                .then(res => res.json())
                .then(data => this.relateds = data.filter(p => p.comment_count > 3))
                .catch(err => console.log(err));
        }
    },
    created() {
        this.getUser();
    },
}
</script>

<style scoped>
#app {
    background-color: #FAFAFA;
    font-family: Arial, Helvetica, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}

footer {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 4em;
}

footer img {
    width: 7em;
}

#content {
    max-width: 950px;
    margin: 0 auto;
    padding: 15px;
}

.related-posts {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-gap: 35px;
}

p {
    margin: 15px auto;
    font-family: Arial;
    font-style: normal;
    font-weight: bold;
    color: #8E8E8E;
}

hr {
    margin-top: 60px;
}

@media only screen and (max-width: 750px) {
    .related-posts {
        grid-template-columns: 1fr 1fr !important;
        grid-gap: 20px !important;
    }

    footer {
        padding: 2em !important;
    }
}

@media only screen and (max-width: 450px) {
    .related-posts {
        grid-template-columns: 1fr !important;
        grid-gap: 10px !important;
    }

    footer {
        padding: 1em !important;
    }
}
</style>
