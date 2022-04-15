<template>
<div class="app">
    <button v-on:click="addLike">Like</button>
    <button @click="addDislike">Dislike</button>
</div>
    <div>
        <h3> Количество лайков {{likes}} </h3>
        <h3> Количество  дизлайков {{dislikes}} </h3>
    </div>
    <form action="" @submit.prevent> 
        <h4>Создание поста</h4>
        <input 
            v-bind:value="title" 
            @input="title = $event.target.value"
            class="input" 
            type="text" 
            placeholder="Название"
        >
        <input 
            v-bind:value="body" 
            @input="body = $event.target.value"
            class="input" 
            type="text" 
            placeholder="Описание"
        >
        <button @click="createPost">Создать пост</button>
    </form>
    <div class="post" v-for="post in posts">
        <div> <strong>Название: </strong>{{post.title}}</div>
        <div> <strong>Описание: </strong>{{post.body}}</div>
    </div>

</template>
    
<script>
    export default {
        data () {
            return {
                likes: 0, 
                dislikes: 0,
                posts: [
                    {id: 1, title: 'JS', body: 'Описание'},
                    {id: 2, title: 'JS 2', body: 'Описание 2'},
                    {id: 3, title: 'JS 3', body: 'Описание 3'},
                ],
                title: '',
                body: '',
            }
        }, 
        methods: {
            addLike() {
                this.likes += 1
            }, 
            addDislike() {
                this.dislikes += 1
            }, 
            createPost() {
                const newPost = {
                    id: Date.now(),
                    title: this.title,
                    body: this.body,
                }
                this.posts.push(newPost)
                this.title = ''
                this.body = ''
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

    .post {
    padding: 15px;
    border: 2px solid teal;
    margin: 10px 0  0 0 ;
    }

    .input{
        width: 100%;
        border: 1px solid teal;
        padding: 10px 15px;
    }
</style>