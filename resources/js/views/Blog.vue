<template>
    <div>
        <spin v-if="loading"></spin>
        <div class="uk-child-width-1-2@s uk-grid-match" uk-grid v-else>
            <post
                v-for="post in posts"
                :title="post.title"
                :email="post.email"
                :date="post.created_at"
                :body="post.body"
                :key="post.id"
            />
            
        </div>
    </div>
</template>

<script>
    import Spin from "../components/Spin";
    import axios from 'axios';
    import Post from "../components/Blog/Post";
    export default {
        components: {
            Spin,
            Post
        },
        data: () => ({
            loading: true,
            posts: []
        }),
        mounted() {
            this.loadPosts();
        },
        methods: {
            loadPosts() {
                axios.get('/api/posts')
                .then(res => {
                    this.posts = res.data;
                    setTimeout(() => {
                        this.loading = false;
                    }, 500)
                })
            }
        }
    }
</script>

<style scoped>
    .uk-card {
        width: 40%;
        margin-right: 20px;
        margin-bottom: 20px;
    }

    .uk-card:last-child {
        margin-right: 0;
    }
</style>
