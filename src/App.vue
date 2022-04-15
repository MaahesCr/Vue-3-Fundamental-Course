<template>
<div>
    <button v-on:click="addLike">Like</button>
    <button @click="addDislike">Dislike</button>
</div>
    <div>
        <h3> Количество лайков {{likes}} </h3>
        <h3> Количество  дизлайков {{dislikes}} </h3>
    </div>
    <div class="post">
        <div> <strong>Название: </strong>Пост о JS</div>
        <div> <strong>Описание: </strong>JS</div>
    </div>
</template>
    
<script>
    export default {
        data () {
            return {
                likes: 0, 
                dislikes: 0,
            }
        }, 
        methods: {
            addLike() {
                this.likes += 1
            }, 
            addDislike() {
                this.dislikes += 1
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

    .post {
    padding: 15px;
    border: 1px solid teal;
    }
</style>