<template>
    <a class="p-2 text-white font-medium text-sm leading-snug uppercase rounded shadow-md hover:shadow-lg focus:shadow-lg focus:outline-none focus:ring-0 active:shadow-lg transition duration-150 ease-in-out w-full flex justify-center items-center bg-blue-600"
        @click="login" role="button" data-mdb-ripple="true" data-mdb-ripple-color="light">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 488 512" class="h-5 w-5 fill-white mb-1 mr-5">
            <path
                d="M488 261.8C488 403.3 391.1 504 248 504 110.8 504 0 393.2 0 256S110.8 8 248 8c66.8 0 123 24.5 166.3 64.9l-67.5 64.9C258.5 52.6 94.3 116.6 94.3 256c0 86.5 69.1 156.6 153.7 156.6 98.2 0 135-70.4 140.8-106.9H248v-85.3h236.1c2.3 12.7 3.9 24.9 3.9 41.4z" />
        </svg>
        Sign In With google
    </a>
</template>

<script>
import axios from "axios";
import { googleTokenLogin } from "vue3-google-login";
import Swal from 'sweetalert2'
export default {
    methods: {
        login() {
            googleTokenLogin({ clientId: '353283530301-lgl6jhjvg6cr3foc30607b3omfqs2ste.apps.googleusercontent.com' }).then((response) => {
                var url = 'https://www.googleapis.com/oauth2/v3/userinfo?access_token=' + response.access_token;
                axios.get(url).then((res) => {
                    axios.get('http://54.169.143.212/api/userBy/' + res.data.email).then((res) => {
                        axios.post("http://54.169.143.212/api/loginViaGoogle/", { email: res.data.email }).then((res) => {
                            if (res.data.sms == 'Invaliid password') {
                                Swal.fire({
                                    showCancelButton: true,
                                    confirmButtonText: 'Create account',
                                    icon: 'error',
                                    text: "You don't have account yet!"
                                }).then((result) => {
                                    if (result.isConfirmed) {
                                        this.$emit('create-account', true);
                                    }
                                })
                            } else {
                                window.location.assign('/')
                                localStorage.setItem('userId', res.data.id)
                                axios.get('http://54.169.143.212/api/user/' + localStorage.getItem('userId')).then((res) => {
                                    localStorage.setItem('role', res.data[0].role)
                                    console.log(res.data[0]);
                                })
                            }
                        })
                    });
                })
            })
        }
    }
}
</script>


