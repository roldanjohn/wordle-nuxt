<template>
    <div>
        <h1>Register</h1>
        <form @submit="login" class="register-form">
            <div class="register-form__div">
                <label>Username:</label>
                <input v-model="username" type="text" name="username" placeholder="Input username" />
            </div>
            <div class="register-form__div">
                <label>Password:</label>
                <input v-model="password" type="password" name="password" placeholder="Type password here" />
            </div>
            <div class="register-form__div">
                <label>Email:</label>
                <input v-model="password" type="email" name="password" placeholder="Type password here" />
            </div>

            <input type="submit" value="Register" class="btn" />
        </form>
    </div>
</template>

<script>
export default {

}
</script>