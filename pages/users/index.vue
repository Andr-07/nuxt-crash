<template>
    <section>
        <h1>User's page</h1>
        <ul>
            <li v-for="user of users" :key="user.id"> 
                <a href="#" @click.prevent="openUser(user.id)"> {{user.name}}</a>
            </li>
        </ul>
    </section>
</template>

<script>
export default {
    // async asyncData({$axios}) {
    //     const users = await $axios.$get('https://jsonplaceholder.typicode.com/users');
    //     return {users};
    // },
    async fetch({store}) {
        if (store.getters['users/users'].length === 0) {
            await store.dispatch('users/fetch')
        }
    },
    data: () => ({
            pageTitle: []
    }),
    computed: {
        users() {
            return this.$store.getters['users/users']
        }
    },
    // async mounted() {
    //     this.users = await this.$axios.$get('https://jsonplaceholder.typicode.com/users')
    // },
    methods: {
        openUser(user) {
           this.$router.push('/users/' + user) 
        }
    }
}
</script>