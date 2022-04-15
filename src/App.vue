<template>
<div class="app">
    <button v-on:click="addLike">Like</button>
    <button @click="addDislike">Dislike</button>
        <h3> Количество лайков {{likes}} </h3>
        <h3> Количество  дизлайков {{dislikes}} </h3>

        <h1>Страница с постами</h1>
        <my-btn
            @click="showDialog"
            style="margin: 15px 0"
        >Создать пост</my-btn>
        <my-dialog v-model:show="dialogVisable"> 
            <post-form 
                @create=createPost    
            />        
        </my-dialog>

    <post-list 
        v-bind:posts="posts" 
        @remove="removePost"
        v-if="isPostsLoading"
    />
    <div v-else>Идет загрузка...</div>

</div>



</template>
    
<script>
import PostForm from '@/components/PostForm.vue'
import PostList from '@/components/PostList.vue'
import axios from 'axios'

    export default {
        components: {
            PostForm, PostList
        },

        data () {
            return {
                likes: 0, 
                dislikes: 0,
                posts: [],
                dialogVisable: false,
                isPostsLoading: false, 
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
                this.dialogVisable = false;
            },
            removePost(post) {
                this.posts = this.posts.filter(p => p.id !== post.id)
            },
            showDialog(){
                this.dialogVisable=true
            }, 
            async fetchPosts() {
                try {
                    this.isPostsLoading = true
                    setTimeout( async () => {
                        const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10')
                        this.posts = response.data
                        this.isPostsLoading = true
                    }, 1000)
                    console.log(response)
                } catch (e) {
                    //alert('Ошибка: ', e)
                }  finally {
                    this.isPostsLoading = false
                }
            }
        },
        mounted() {
            this.fetchPosts();
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