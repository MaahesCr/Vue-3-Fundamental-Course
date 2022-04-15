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
                dialogVisable: false
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