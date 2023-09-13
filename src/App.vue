<template>
    <div id="app" class="container p-4 ">
        <Search
            class="m-3 "
            v-model="searchValue"
            @search="search"
        />

        <div v-if="postsWithAuthor.length > 0 " class="flex row wrap">
            <PostCard
                class="m-4"
                v-for="post in filteredPosts"
                :key="post.id"
                :post="post"

            />
        </div>
        <h3 v-else>
            Постов пока нет..
        </h3>

    </div>
</template>

<script>

import PostCard from '@/components/PostCard'
import Search from '@/components/Search'
import axios from 'axios';


export default {
    components: {PostCard, Search},
    data: () => ({
        searchValue: null,
        postsWithAuthor: [],
    }),
    mounted() {

        this.fetchPostsWithAuthor()
    },
    methods: {
        async fetchPostsWithAuthor() {
            let posts_data = []
            await axios.get(`https://jsonplaceholder.typicode.com/posts`)
                .then(response => {
                    const posts = response.data
                    let fetchedUsers = []
                    posts.forEach((post) => {
                        fetchedUsers.push(
                            axios.get(`https://jsonplaceholder.typicode.com/users/${post.userId}`)
                                .then(response => {
                                    const user = response.data
                                    post["userName"] = user.name;
                                    posts_data.push(post);
                                })
                        )
                    })

                })
            Promise.all(posts_data).then(() => {
                this.postsWithAuthor = posts_data;
            })
        },
        search(value) {
            this.searchValue = value
            console.log('changeValueParent', this.searchValue)
        },
    },
    computed: {
        filteredPosts() {
            if (this.searchValue) {
                return this.postsWithAuthor.filter(post => {
                    return post.userName.toLowerCase().includes(this.searchValue.toLowerCase());
                })
            } else {
                return this.postsWithAuthor
            }


        },
    },
}
</script>

<style scoped>

</style>
