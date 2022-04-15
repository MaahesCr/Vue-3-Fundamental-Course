<template>
<div class="app">
    <button v-on:click="addLike">Like</button>
    <button @click="addDislike">Dislike</button>
    
        <h3> Количество лайков {{likes}} </h3>
        <h3> Количество  дизлайков {{dislikes}} </h3>
    <post-form 
        @create=createPost    
    />
    <post-list 
    v-bind:posts="posts" 
    @remove="removePost"
    />

</div>



</template>
    
<script>
import PostForm from '@/components/PostForm.vue'
import PostList from '@/components/PostList.vue'

    export default {
        components: {
            PostForm, PostList
        },

        data () {
            return {
                likes: 0, 
                dislikes: 0,
                posts: [
                    {id: 1, title: 'JS', body: 'Описание'},
                    {id: 2, title: 'JS 2', body: 'Описание 2'},
                    {id: 3, title: 'JS 3', body: 'Описание 3'},
                ],
            }
        }, 
        methods: {
            addLike() {
                this.likes += 1
            }, 
            addDislike() {
                this.dislikes += 1
            }, 
            createPost(post, second) {
                console.log(post)
                console.log(second)
                this.posts.push(post) 
            },
            removePost(post) {
                this.posts = this.posts.filter(p => p.id !== post.id)
            }
        }
    }
</script>

<style>
    * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    }

    .app {
        padding: 20px;
    }
</style>