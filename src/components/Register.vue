<template>
      <div class="omc-register">
        <div class="omc-register-form">
            <label>First Name</label>
            <input v-model="formData.firstname" type="text">
            <label>Last Name</label>
            <input v-model="formData.lastname" type="text">
            <label>Email</label>
            <input v-model="formData.email" type="text">
            <label>Password</label>
            <input v-model="formData.password" type="text">
            <label>Confirm Password</label>
            <input v-model="formData.password_confirmation" type="text">
            <div class="omc-register-form-controls">
                <a @click.prevent="register" href="#">Register</a>
                <router-link to="/login">Back to login</router-link>
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
                    firstname: '',
                    lastname: '',
                    email: '',
                    password: '',
                    password_confirmation: ''
                }
            }
        },
        methods: {
            register() {
                axios.post('http://api.omc.com/oauth/token', {
                    grant_type: 'client_credentials',
                    client_id: '1',
                    client_secret: '4teAR9JQJz4jZIL9VE9QCWr0RXjhLpzs6YgFkjlb'
                }).then((response) => {
                    const accessToken = response.data.access_token;

                    axios({
                        method: 'post',
                        url: 'http://api.omc.com/users', 
                        data: this.formData,
                        headers: { 'Authorization': `Bearer ${accessToken}` }
                    });
                });
            }
        }
    }
</script>


<style scoped lang="scss">
.omc-register {
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