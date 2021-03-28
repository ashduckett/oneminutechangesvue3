<template>
    <div class="omc-login">
        <div class="omc-login-form">
            <label>Email</label>
            <input v-model="formData.email" type="text">
            <label>Password</label>
            <input v-model="formData.password" type="text">
            <div class="omc-login-form-controls">
                <a @click="login" href="#">Submit</a>
                <router-link to="/register">Sign Up</router-link>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            formData: {
                email: '',
                password: ''
            }
        }
    },
    methods: {
        login() {
            axios.post('http://api.omc.com/oauth/token', {
                grant_type: 'password',
                client_id: '2',
                client_secret: 'wUK3jZz5ydaDbg4D2OQ6m4m8wi10b3y3yzWxRd1y',
                username: this.formData.email,
                password: this.formData.password
            }).then((response) => {
                axios({
                    method: 'get',
                    url: 'http://api.omc.com/users/me',
                    headers: {
                        'Authorization': `Bearer ${response.data.access_token}`
                    }
                }).then((response) => {
                    console.log(response);
                });
            });
        }
    }
}
</script>

<style scoped lang="scss">
.omc-login {
    background-color: beige;
    height: 100%;
    &-form {
        display: flex;
        flex-direction: column;
        margin: auto;
        width: 20%;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        position: absolute;
    }
}
</style>

