<template>
<div class="app">
    <button v-on:click="addLike">Like</button>
    <button @click="addDislike">Dislike</button>
        <h3> Количество лайков {{likes}} </h3>
        <h3> Количество  дизлайков {{dislikes}} </h3>

        <h1>Страница с постами</h1>
        <my-input
            v-model="searchQuery"
            placeholder="Поиск по заголовку"
        />
        <div class="app__btns">
            <my-btn
                @click="showDialog"
            >Создать пост</my-btn>
            <my-select 
            v-model="selectedSort"
            :options="sortOptions"
            /> 
        </div>
        <my-dialog v-model:show="dialogVisable"> 
            <post-form 
                @create=createPost    
            />        
        </my-dialog>

    <post-list 
        v-bind:posts="sortedEndSearchedPosts" 
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
                selectedSort: '',
                searchQuery: '',
                sortOptions: [
                    {value: 'title', name: 'По названию', },
                    {value: 'body', name: 'По описанию', }
                ]
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
            }, 
        },
        mounted() {
            this.fetchPosts();
        },
        
        computed: {
            sortedPosts(){
                return [...this.posts].sort((post1, post2) => {
                    return post1[this.selectedSort]?.localeCompare(post2[this.selectedSort])
                })
            },
            sortedEndSearchedPosts(){
                return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
            }
        },

        watch: {
            /*
            selectedSort(newValue) {
                this.posts.sort((post1, post2) => {
                    return post1[newValue]?.localeCompare(post2[newValue])
                })
            }
            */
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

    .app__btns{
        display: flex;
        justify-content: space-between;
        margin: 15px 0
    }
</style>