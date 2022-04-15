<template>
    <form action="" @submit.prevent> 
        <h4>Создание поста</h4>
        <input 
            v-model="post.title"
            class="input" 
            type="text" 
            placeholder="Название"
        >
        <input 
            v-model="post.body"
            class="input" 
            type="text" 
            placeholder="Описание"
        >
        <my-btn @click="createPost">
        Создать пост
        </my-btn>
    </form>
</template>

<script>
import MyBtn from './UI/MyBtn.vue'
    export default {
  components: { MyBtn },
        data () {
            return {
                post: {
                    title: '',
                    body: '',
                }
            }
        }, 
        methods: {
            createPost() {
                this.post.id = Date.now()
                this.$emit('create', this.post, 'second')
                this.post = {
                    title: '',
                    body: '',
                }
            }
        }
    }
</script>

<style scoped>
    .input{
        width: 100%;
        border: 1px solid teal;
        padding: 10px 15px;
    }
</style>