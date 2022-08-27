<template>
<div>
    <h1>Login</h1>
    <form @submit.prevent="handleLogin">
        <input type="email" placeholder="Email" v-model="email" required>
        <input type="password" placeholder="Password" v-model="password" required>

        <button type="submit">Login</button>

        <router-link to="/register" class="question">Don't have an account?</router-link>

        <div class="errors" v-for="error in errors" :key="error">
            {{ error }}
        </div>
    </form>
</div>
    
</template>

<script>
export default {
    data(){
        return {
            errors: [],
            email: '',
            password: '',
            user: {}
        }
    },
    methods: {
        handleLogin() {
            fetch('http://localhost:3000/users')
            .then(data => data.json())
            .then(json => {
                json.forEach(element => {
                    if(this.email == element.email && this.password == element.password) {
                        this.user = element
                        console.log(this.user)
                        this.$emit('loggedIn', this.user)
                        this.$router.push('/')
                    }
                });
                this.user != 0 ? this.errors.push("Account doesn't exist") : ''
            })
        }
    }

}
</script>

<style>

</style>