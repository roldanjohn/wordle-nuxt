<template>
    <div>
        <h1>Login</h1>
        <form @submit="login" class="login-form">
            <div class="login-form__div">
                <label>Username:</label>
                <input v-model="username" type="text" name="text" placeholder="Input username" />
            </div>
            <div class="login-form__div">
                <label>Password:</label>
                <input v-model="password" type="text" name="day" placeholder="Type password here" />
            </div>

            <input type="submit" value="Login" class="btn" />
        </form>
    </div>
</template>

<script>
export default {
    name: "Login",
    data(){
        return {
            username: '',
            password: '',
        }
    }
}
</script>

<style scoped>
*{
    display: flex;
    flex-flow: column wrap;
    align-items: center;
}

.login-form__div{
    width: 60%;
}
</style>