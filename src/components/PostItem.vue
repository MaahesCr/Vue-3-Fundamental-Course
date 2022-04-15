<template>
    <div class="post">
        <div>
            <div> <strong>Название: </strong>{{post.title}}</div>
            <div> <strong>Описание: </strong>{{post.body}}</div>
        </div>
        <div class="post__btns">
            <my-btn
            @click="$emit('remove', post)"
            >Удалить</my-btn>
        </div>
    </div>
</template>

<script>
import MyBtn from './UI/MyBtn.vue'
    export default {
  components: { MyBtn },
        props: {
            post: {
                type: Object,
                required: true
            }
        }
    }
</script>

<style scoped>
    .post {
    padding: 15px;
    border: 2px solid teal;
    margin: 10px 0  0 0 ;
    display: flex;
    align-items: center;
    justify-content: space-between;
    }
</style>