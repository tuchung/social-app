<template>
    <b-container>
        <b-container class='login-container'>
        <alert v-bind="message"></alert>    
        <h1><b-badge variant="info">Welcome</b-badge></h1>    
        <b-form>
        <b-form-group id="login-email-group"
                        label="Email address:"
                        label-for="login-email">
            <b-form-input id="login-email"
                        type="email"
                        v-model="form.email"
                        placeholder="Enter Email"
                        required>
            </b-form-input>
        </b-form-group>
        <b-form-group id="login-password-group"
                        label="Password:"
                        label-for="login-password">
            <b-form-input id="login-password"
                        type="password"
                        v-model="form.password"
                        required
                        placeholder="Enter password">
            </b-form-input>
        </b-form-group>
        <b-button @click="submitForm" variant="primary">Login</b-button>
        </b-form>
        </b-container>

        <b-container class="login-container">
                <h3><b-badge variant="warning">Don't Have An Account With Us?</b-badge></h3>
                <div><router-link to="/login/register"><a>Click here to Register</a></router-link></div>
                <div><router-link to="/"><a>Forgot/Reset Password</a></router-link></div>
        </b-container>
    </b-container>
    
</template>

<script>
    import alert from '../helpers/Alert' 

    export default {
        Name: 'Login',
        data() {
           return {
               message: {
                    trigger: false
               },
               form: {
                   email: '',
                   password: ''
               }
           }     
        },
        methods: {
            submitForm(){
                let vm = this; 
                axios.post('/login',vm.form)
                .then(function(response) {
                    console.log(response);
                    vm.$router.push({
                        path: '/dashboard'
                    });
                })
                .catch(error =>  {
                    console.log(error);
                    this.message = {
                        type : 'danger',
                        message : error.response.data,
                        trigger: !vm.message.trigger
                    }
                });    
            }
        },
        mounted() {
        },
        components: {alert}
    }
</script>

<style scoped>
    .login-container{
        margin-top: 50px;
    }
</style>
