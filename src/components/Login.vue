<template>  
    <div>    
        <h2>Login</h2>    
        <form v-on:submit="login">    
            <input type="text" name="email" /><br>    
            <input type="password" name="password" /><br>    
            <input type="submit" value="Login" />    
        </form>    
    </div>
</template>

<script>  
    import router from "../router"    
    import axios from "axios"    
    export default {    
        name: "Login",    
        methods: {    
            login: (e) => {    
                e.preventDefault()   
                let login = () => {    
                    let data = {    
                        email: e.target.elements.email.value,    
                        password: e.target.elements.password.value      
                    }    
                    axios.post("/api/login", data)    
                        .then((response) => {    
                            console.log(response.data.data) 
                            localStorage.setItem('token', response.data.data.token);
                            router.push("/dashboard")
                        })    
                        .catch((errors) => {    
                            console.log("Cannot log in")    
                        })    
                }    
                login()    
            }    
        }    
    }
</script>