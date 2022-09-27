<template>
    <div>
        <div class="container">
            <h1 class="p-3 m-3">
                Recent posts:
            </h1>
            <div class="row">

                    <Card v-for="post in posts" :key="post.id" :post="post"/>

            </div>
        </div>
    </div>
</template>

<script>
    import axios from 'axios';
    import Card from './Card.vue';

export default {
    components:{
        Card
    },

    data:function(){
        return{
            posts : [],
            currentPage: 1,
            lastPage: null,
            loading : false,
        }
    },
    methods: {
        getPosts(postsPage = 1){
            axios.get('/api/posts',{
                page: postsPage
            }).then((response) => {
                this.posts = response.data.results.data;
                this.currentPage = response.data.results.current_page;
                this.lastPage = response.data.results.last_page;
                this.loading = false;
            }).catch((error) => {
                console.error(error);
            })
        }
    },
    created(){
        this.getPosts()
    }

};
</script>

<style>

</style>
