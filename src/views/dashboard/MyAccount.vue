<template>
    <div class="container">
        <div class="columns is-multiline">
            <div class="column is-12">
                <h1 class="title">My Account</h1>
            </div>

            <div class="column is-12">
                <div class="buttons">
                    <button @click="logout()" class="button is-danger">Log out</button>
                </div>
            </div>

        </div>
    </div>    
</template>

<script>
    import axios from 'axios'
    import {toast} from 'bulma-toast'

    export default {
        name: 'MyAccount',
        methods: {
            async logout() {
                const formData = {
                    user_id: this.$store.state.user.id,
                }
                await axios
                    .post('http://127.0.0.1:8000/api/logout/', formData)
                    .then(response => {
                        console.log('logout')
                        axios.defaults.headers.common['Authorization'] = ''     
                        localStorage.removeItem('token')
                        this.$store.commit('removeToken')
                        this.$router.push('/log-in')
                    })
                    .catch(
                        error => {
                            console.log(JSON.stringify(error));
                        }
                    )
            }
        }
    }
</script>

<style scoped>
    .btn-leads {
        margin-right: 10px;
    }
</style>