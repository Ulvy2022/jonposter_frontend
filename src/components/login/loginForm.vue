<template>
    <section class=" bg-gray-200 " style="height:89vh;">
        <div class="container px-6 py-12 h-full animate__zoomIn animate__animated">
            <!-- <p>Welcome to my codepen profile</p> -->
            <div class="flex justify-center items-center flex-wrap g-6 text-gray-800">
                <div class=" w-full lg:w-5/12  lg:ml-20  bg-white p-5 rounded-lg">
                    <p class="w-full flex justify-center items-center text-2xl text-blue-500 mb-4 ">
                        Welcome back</p>
                    <div class="relative mb-5">
                        <div class="flex absolute inset-y-0 left-0 items-center pl-3 pointer-events-none">
                            <svg aria-hidden="true" class="w-5 h-5 text-gray-500 dark:text-gray-400" fill="currentColor"
                                viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                                <path d="M2.003 5.884L10 9.882l7.997-3.998A2 2 0 0016 4H4a2 2 0 00-1.997 1.884z"></path>
                                <path d="M18 8.118l-8 4-8-4V14a2 2 0 002 2h12a2 2 0 002-2V8.118z"></path>
                            </svg>
                        </div>
                        <input type="text" v-model="email"
                            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full pl-10 p-3 "
                            placeholder="Email">
                    </div>

                    <div class="mb-2">
                        <div class="flex">
                            <span v-if="isEmptyEmail" class="text-red-700 animate__headShake animate__animated">Email
                                cannot be empty</span>
                        </div>
                    </div>

                    <!-- password -->
                    <div class="relative">
                        <div class="flex absolute inset-y-0 left-0 items-center pl-3 pointer-events-none">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 fill-gray-500" viewBox="0 0 448 512">
                                <path
                                    d="M144 144v48H304V144c0-44.2-35.8-80-80-80s-80 35.8-80 80zM80 192V144C80 64.5 144.5 0 224 0s144 64.5 144 144v48h16c35.3 0 64 28.7 64 64V448c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V256c0-35.3 28.7-64 64-64H80z" />
                            </svg>
                        </div>
                        <input :type="type" id="email-address-icon" v-model="password" @keyup.enter="signIn()"
                            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full pl-10 p-3  "
                            placeholder="Password">
                    </div>
                    <div class=" mt-4 mb-2">
                        <div class="flex" v-if="isEmptyPassword">
                            <span class="text-red-700 animate__headShake animate__animated">Password cannot be
                                empty</span>
                        </div>
                    </div>
                    <div class=" -mt-4 mb-2">
                        <div class="flex" v-if="showInvalid">
                            <span class="text-red-700 animate__headShake animate__animated">Invalid Password or
                                Email!</span>
                        </div>
                    </div>

                    <div class="flex justify-between items-center mb-6 mt-7">

                        <div class="flex items-start">
                            <div class="flex items-center h-5">
                                <input @click="showPassword()" id="remember" type="checkbox"
                                    class="w-4 h-4 border border-gray-300 rounded bg-gray-50 focus:ring-3 focus:ring-primary-300 dark:bg-gray-700 dark:border-gray-600 dark:focus:ring-primary-600 dark:ring-offset-gray-800">
                            </div>
                            <div class="ml-3 text-sm">
                                <label for="remember" class="text-gray-500 dark:text-gray-300">Show password</label>
                            </div>
                        </div>

                        <a @click="forgotPassword"
                            class="cursor-pointer hover:underline hover:underline-offset-1 text-blue-600 hover:text-blue-700 focus:text-blue-700 active:text-blue-800 duration-200 transition ease-in-out">Forgot
                            password?</a>
                    </div>

                    <!-- Submit button -->
                    <button type="submit" v-if="!isClickSigIn" @click="signIn()"
                        class="inline-block px-7 py-3 bg-blue-600 text-white font-medium text-sm leading-snug uppercase rounded shadow-md  w-full"
                        data-mdb-ripple="true" data-mdb-ripple-color="light">
                        Sign in
                    </button>

                    <!-- <p class="text-sm font-light lg:hidden mt-3  text-gray-500 dark:text-gray-400"
                        @click="show_register()">
                        Don???t have an account yet? <a href="#"
                            class="font-medium text-blue-500 hover:underline hover:underline-offset-2 dark:text-primary-500">Sign
                            up</a>
                    </p> -->
                    <button v-if="isClickSigIn" class="btn loading bg-blue-600 w-full">Sign In</button>

                    <div
                        class="flex items-center my-4 before:flex-1 before:border-t before:border-gray-300 before:mt-0.5 after:flex-1 after:border-t after:border-gray-300 after:mt-0.5">
                        <p class="text-center font-semibold mx-4 mb-0">OR</p>
                    </div>
                    <vue-github username="harps116" />
                    <googleLoginForm @create-account="is_show = true;" />

                    <div class="flex items-center justify-center">
                        <span class="text-black-500">Don???t have an account yet?</span>
                        <router-link to="/signup"
                            class="text-black-300 p-1 rounded hover:underline block mt-4 lg:inline-block active text-blue-600 lg:mt-0 mr-4">
                            Sign Up
                        </router-link>
                    </div>
                </div>
            </div>

            <Password-Form v-if='pass_show'>
                <div class="modal-mask">
                    <div class="modal-wrapper w-full">
                        <form @submit.prevent='' class='w-[40%] m-auto mt-64 rounded px-8 pt-6 pb-8 mb-4 bg-blue-200'>
                            <p>Please input your password: It must be 6 characters at least</p>
                            <div class="flex flex-col mb-2 w-full">
                                <div class="relative">
                                    <input placeholder="Password" :type="showPass ? 'password' : 'text'"
                                        class="peer shadow appearance-none border mr-2 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                                        v-model="passwordGoogle">

                                    <div class="absolute inset-y-0 right-0 pr-3 flex items-center text-sm leading-5">

                                        <svg class="h-5 w-5 text-black" @click="showPass = !showPass" width="24"
                                            height="24" viewBox="0 0 24 24"
                                            :class="{ 'hidden': !showPass, 'block': showPass }" stroke-width="2"
                                            stroke="currentColor" fill="none" stroke-linecap="round"
                                            stroke-linejoin="round">
                                            <path stroke="none" d="M0 0h24v24H0z" />
                                            <circle cx="12" cy="12" r="2" />
                                            <path d="M2 12l1.5 2a11 11 0 0 0 17 0l1.5 -2" />
                                            <path d="M2 12l1.5 -2a11 11 0 0 1 17 0l1.5 2" />
                                        </svg>

                                        <svg class="h-5 w-5 text-black" @click="showPass = !showPass" fill="none"
                                            viewBox="0 0 24 24" :class="{ 'block': !showPass, 'hidden': showPass }"
                                            stroke="currentColor">
                                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                                d="M13.875 18.825A10.05 10.05 0 0112 19c-4.478 0-8.268-2.943-9.543-7a9.97 9.97 0 011.563-3.029m5.858.908a3 3 0 114.243 4.243M9.878 9.878l4.242 4.242M9.88 9.88l-3.29-3.29m7.532 7.532l3.29 3.29M3 3l3.59 3.59m0 0A9.953 9.953 0 0112 5c4.478 0 8.268 2.943 9.543 7a10.025 10.025 0 01-4.132 5.411m0 0L21 21" />
                                        </svg>
                                    </div>
                                </div>
                            </div>

                            <button @click="registerByGoogleLast"
                                class="bg-blue-500 w-full  hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none m-auto focus:shadow-outline"
                                type="submit">Register</button>
                        </form>
                    </div>
                </div>
            </Password-Form>
        </div>
    </section>

</template>

<script>
import axios from "axios"
// import registerForm from '../slot/generalSlot.vue';
import googleLoginForm from '../google/googleLogin.vue';
import passwordForm from '../slot/generalSlot.vue'
export default {
    components: {
        // 'Register-Form': registerForm,
        'Password-Form': passwordForm,
        googleLoginForm,
    },

    data() {
        return {
            progress: 0,
            pass_show: false,
            is_show: false,
            showInvalid: false,
            type: 'password',
            isClickSigIn: false,
            isInval: 'Invalid email address or password!',
            isEmptyEmail: false,
            isEmptyPassword: false,
            registerValidation: false,
            role: 'user',
            isNoPass: false,
            isFirstNameEmpty: false,
            email: '',
            password: '',



            // ==========Register=======
            showPass: false,
            showConfirmPassword: false,
            fullName: '',
            emailUser: '',
            passwordUser: '',
            passwordUserConfirm: '',
            isFormComplete: false,
            passwordGoogle: '',
            fullNameGoogle: '',
            emailGoogle: '',
            gender: '',
            dataRegisterViaGoo: {},
        }
    },
    methods: {
        show_register() {
            this.is_show = true;
        },

        checkInput(input) {
            if (input.trim() == '') {
                return '';
            }
        },

        checkPassword(pass) {
            if (pass.trim() == '') {
                return this.isNoPass = true;
            }
        },

        // Register===============
        handleFormSubmit() {
            console.log('submit')
        },

        signIn() {
            if (!this.email.trim() == '' && !this.password.trim() == '') {
                this.isClickSigIn = true
                this.isEmptyEmail = false
                this.isEmptyPassword = false
                axios.post('http://54.169.143.212/api/login/',
                    { email: this.email, password: this.password }).then((res) => {
                        if (res.data.sms == 'Invalid password') {
                            this.showInvalid = true
                            this.isClickSigIn = !this.isClickSigIn
                        } else {
                            localStorage.setItem('userId', res.data.id)
                            localStorage.setItem('role', res.data.role)
                            localStorage.setItem('subscription', res.data.subscription)
                            axios.post("http://54.169.143.212/api/trail", { subscriber_id: res.data.id, plan_id: 1 }).then(() => {
                                this.showInvalid = false;
                                window.location.assign('/')
                            })
                        }
                    }).catch(() => {
                        this.isClickSigIn = !this.isClickSigIn
                    })
            }

            if (this.email == '') {
                this.isEmptyEmail = true
            }
            if (this.password.trim() == '') {
                this.isEmptyPassword = true
            }
            if (this.email.trim() != '') {
                this.isEmptyEmail = false
                this.showInvalid = !this.showInvalid

            }
            if (this.password.trim() != '') {
                this.isEmptyPassword = false
                this.showInvalid = !this.showInvalid
            }
        },

        showPassword() {
            if (this.type == 'text') {
                this.type = 'password'
            } else {
                this.type = 'text'
            }
        },

        forgotPassword() {
            this.$router.push('/resetPsw');
        },

        checkRegisterInput(input) {
            if (input.trim() == '') {
                return input = null;
            }
        },
    },

    mounted() {
        if (this.$route.params.id != undefined) {
            console.log(this.$route.params.id);
            axios.put("http://127.0.0.1:8000/api/verifyemail/" + this.$route.params.id)
                .then((res) => {
                    console.log(res.data);
                })
        }
    }
}

</script>


<style scoped>
.input {
    transition: border 0.2s ease-in-out;
    min-width: 280px
}

.input:focus+.label,
.input:active+.label,
.input.filled+.label {
    font-size: .75rem;
    transition: all 0.2s ease-out;
    top: -0.9rem;
    background-color: #fff;
    color: #1a73e8;
    padding: 0 5px 0 5px;
    margin: 0 5px 0 5px;
}

.label {
    transition: all 0.2s ease-out;
    top: 0.1rem;
    left: 0;
}

input[type=email]:not(:placeholder-shown):invalid {
    color: red;
    outline-color: red;
}

input[type=email]:not(:placeholder-shown):valid {
    color: green;
    outline-color: green;
}
</style>