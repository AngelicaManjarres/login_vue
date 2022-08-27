<template>
<div>
    <h1>Register</h1>

    <form @submit.prevent="handleRegister">
        <input type="text" placeholder="Name" v-model="name" required>
        <input type="email" placeholder="Email" v-model="email" required>
        <input type="password" placeholder="Password" v-model="password" required>
        <input type="password" placeholder="Confirm password" v-model="repassword">

        <button type="submit">Register</button>

        <router-link to="/login" class="question">Already have an account?</router-link>

        <!-- Error message -->
        <div class="errors" v-for="error in errors" :key="error">
            {{ error }}
        </div>

        <!-- Success message -->
        <div v-if="success">
            <p class="success"> {{ success }} </p>
        </div>
        

    </form>

</div>
  
</template>

<script>
export default {
    data(){
        return {
            name: '',
            email: '',
            password: '',
            repassword: '',
            success: '',
            errors: []
        }
    },
    methods: {
        handleRegister(){
            this.errors = []
            //Regex validations
            this.name.match(/^[a-zA-Z ]*$/) ? "" : this.errors.push("Please enter a valid name")
            this.email.match(/^[\w-\.]+@([\w-]+\.)+[\w-]{2,4}$/) ? "" : this.errors.push("Please enter a valid email")
            this.password.match(/^(?=.*\d)(?=.*[a-z])(?=.*[A-Z])(?=.*[a-zA-Z]).{8,16}$/) ? "" : this.errors.push("The password must have a special character and must be at least 8 characters long")
            this.password === this.repassword ? "" : this.errors.push("Passwords don't match")

            //Send post request
            if(this.errors.length < 1) {
                console.log(`Your name is ${this.name}, your email is ${this.email} and your passwords is ${this.password}`)

                fetch("http://localhost:3000/users", {
                    method: 'post',
                    headers: {'Content-Type': 'application/json'},
                    body: JSON.stringify({
                        name: this.name,
                        email: this.email,
                        password: this.password})
                    }
                ).then(() => {
                    this.success = "You've been registered succesfully"
                }).catch(err => console.log(err))

            }

        }
    }

}
</script>

<style>
form {
    width: 50vw;
    margin: 2rem auto;
    padding: 2rem 3rem;
    background: #eee;
}

input {
    width: 90%;
    border: none;
    padding: 5px;
    font-size: 1rem;
    margin-top: 1rem;
}

button {
    padding: 10px 15px;
    margin-top: 2rem;
    border: none;
    background: #23ce23;
    color: #fff;
    font-size: 1rem;
}

.question {
    display: block;
    margin-top: 1rem;
}

.errors {
    color: #fff;
    margin-top: 5px;
    text-align: left;
    background: rgb(235, 92, 92);
    padding: 8px;
    font-size: .8rem;
    font-weight: bold;
}

.success {
    color: #fff;
    margin-top: 5px;
    text-align: left;
    background: rgb(51, 224, 89);
    padding: 8px;
    font-size: .8rem;
    font-weight: bold;
}

</style>