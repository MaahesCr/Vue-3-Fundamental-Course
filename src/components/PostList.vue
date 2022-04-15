<template>
    <div v-show="posts.length > 0">
        <h3>Список пользователей</h3>    
        <post-item 
        v-for="post in posts"
        :post="post"
        :key="post.id"
        @remove="$emit('remove', post)"
        />
    </div>
    <div v-show="posts.length === 0">
        <h2 style="color: red">Список постов пуст</h2>
    </div>
</template>

<script>
import PostItem from './PostItem.vue'
    export default {
        components: {
            PostItem
        },
        props: {
            posts: {
                type: Array,
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
    }
</style>