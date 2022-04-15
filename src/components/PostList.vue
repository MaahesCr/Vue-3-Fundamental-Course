<template>
    <div v-show="posts.length > 0">
        <h3>Список пользователей</h3>    
        <transition-group name="user-list">
        <post-item 
        v-for="post in posts"
        :post="post"
        :key="post.id"
        @remove="$emit('remove', post)"
        />
        </transition-group>
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

    .user-list-item {
  display: inline-block;
  margin-right: 10px;
}
.user-list-enter-active,
.user-list-leave-active {
  transition: all 0.4s ease;
}
.user-list-enter-from,
.user-list-leave-to {
  opacity: 0;
  transform: translateX(130px);
}

.user-list-move{
    transition: transform 0.4s ease;
}
</style>