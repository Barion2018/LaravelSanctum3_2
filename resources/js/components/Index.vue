<!--<template>-->
<!--    <div>-->
<!--        <router-link :to="{ name: 'get.index' }">Get</router-link>-->
<!--        <router-link :to="{ name: 'user.login' }">Login</router-link>-->
<!--        <router-link :to="{ name: 'user.registration' }">Registration</router-link>-->
<!--        <router-view></router-view>-->
<!--    </div>-->
<!--&lt;!&ndash;    <div>&ndash;&gt;-->
<!--&lt;!&ndash;        <div class="flex justify-between p-8 w-96 mx-auto">&ndash;&gt;-->

<!--&lt;!&ndash;            <router-link v-if="!token" :to="{ name: 'user.login'}">Login</router-link>&ndash;&gt;-->
<!--&lt;!&ndash;            <router-link v-if="token" :to="{ name: 'user.index'}">Users</router-link>&ndash;&gt;-->
<!--&lt;!&ndash;            <router-link v-if="token" :to="{ name: 'user.feed'}">Feed</router-link>&ndash;&gt;-->
<!--&lt;!&ndash;            <router-link v-if="token" :to="{ name: 'user.personal'}">Personal</router-link>&ndash;&gt;-->
<!--&lt;!&ndash;            <router-link v-if="!token" :to="{ name: 'user.registration'}">Registration</router-link>&ndash;&gt;-->
<!--&lt;!&ndash;            <a v-if="token" @click.prevent="logout" href="#">Logout</a>&ndash;&gt;-->
<!--&lt;!&ndash;        </div>&ndash;&gt;-->

<!--&lt;!&ndash;        <router-view></router-view>&ndash;&gt;-->
<!--&lt;!&ndash;    </div>&ndash;&gt;-->


<!--</template>-->

<!--<script>-->
<!--export default {-->
<!--    name: "Index"-->
<!--}-->
<!--</script>-->

<!--<style scoped>-->

<!--</style>-->
<template>
    <div>
        <div class="flex justify-between p-8 w-96 mx-auto">

            <router-link :to="{ name: 'user.login'}">Login</router-link>
            <router-link  :to="{ name: 'user.registration'}">Registration</router-link>

        </div>

        <router-view></router-view>
    </div>
</template>

<script>
export default {
    name: "Index",
    data() {
        return {
            token: null
        }
    },

    mounted() {
        this.getToken()
    },

    watch: {
        $route(to, from) {
            this.getToken()
        }
    },

    methods: {

        getToken() {
            this.token = localStorage.getItem('x_xsrf_token')
        },

        logout() {
            axios.post('/logout')
                .then( res => {
                    localStorage.removeItem('x_xsrf_token')
                    this.$router.push({name: 'user.login'})
                })
        }
    }
}
</script>

<style scoped>

</style>
