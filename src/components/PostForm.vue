<template>
    <form action="" @submit.prevent> 
        <h4>Создание поста</h4>
        <my-input
            v-model="post.title"
            type="text" 
            placeholder="Название"
        />
        <my-input
            v-model="post.body"
            type="text" 
            placeholder="Описание"
        />
        <my-btn @click="createPost">
        Создать пост
        </my-btn>
    </form>
</template>

<script>
import MyBtn from './UI/MyBtn.vue'
import MyInput from './UI/MyInput.vue'
    export default {
  components: { MyBtn, MyInput },
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

</style>