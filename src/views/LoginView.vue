<script setup>
import { RouterLink} from 'vue-router';
import { reactive, ref} from 'vue';

const data = reactive({})
let welcomePageShow = ref(false)
let message = ref('')
const users = reactive({})

function signIn(){
	Object.assign(users, JSON.parse(localStorage.getItem('users')))

	if(users.email == data.email && users.password == data.password){
		welcomePageShow.value = true
	}else{
		welcomePageShow.value = false
		message.value = "Username/Password Wrong"
	}
}
</script>

<template>
<div  class="min-h-screen flex  justify-center py-12 px-4 sm:px-6 lg:px-8 bg-gray-500 bg-no-repeat bg-cover relative items-center" style="background-image: url(https://images.unsplash.com/photo-1525302220185-c387a117886e?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1950&q=80);">
	<div class="absolute bg-black opacity-60 inset-0 z-0"></div>
	<div v-show="!welcomePageShow" class="max-w-md w-full space-y-8 p-10 bg-white rounded-xl z-10">
		<div class="text-center">
			<h2 class="mt-6 text-3xl font-bold text-gray-900">
				Login Page
			</h2>
			<p class="mt-2 text-sm text-red-600">{{ message }}</p>
		</div>
		<form class="mt-8 space-y-6" action="#" method="POST">
			<input type="hidden" name="remember" value="true">
			<div class="relative">
				<label class="text-sm font-bold text-gray-700 tracking-wide">Email</label>
				<input v-model="data.email" class=" w-full text-base py-2 border-b border-gray-300 focus:outline-none focus:border-indigo-500" type="email" placeholder="mail@gmail.com">
      </div>
      
			<div class="mt-8 content-center">
				<label class="text-sm font-bold text-gray-700 tracking-wide">Password</label>
				<input v-model="data.password" type="password" class="w-full content-center text-base py-2 border-b border-gray-300 focus:outline-none focus:border-indigo-500"  placeholder="Enter your password">
      </div>

			<div class="flex items-center justify-between">
        <div class="flex items-center">
          <input id="remember_me" name="remember_me" type="checkbox" class="h-4 w-4 bg-indigo-500 focus:ring-indigo-400 border-gray-300 rounded">
          <label for="remember_me" class="ml-2 block text-sm text-gray-900">Remember me</label>
        </div>
				<div class="text-sm">
					<RouterLink to="forgot-password" class="font-medium text-indigo-500 hover:text-indigo-500">Forgot your password?</RouterLink>
				</div>
			</div>
			<div>
				<button @click.prevent="signIn()" type="submit" class="w-full flex justify-center bg-indigo-500 text-gray-100 p-4  rounded-full tracking-wide font-semibold  focus:outline-none focus:shadow-outline hover:bg-indigo-600 shadow-lg cursor-pointer transition ease-in duration-300">Sign in</button>
			</div>
			<p class="flex flex-col items-center justify-center mt-10 text-center text-md text-gray-500">
				<span>Don't have an account?</span>
				<RouterLink to="register" class="text-indigo-500 hover:text-indigo-500no-underline hover:underline cursor-pointer transition ease-in duration-300">Sign up</RouterLink>
			</p>
		</form>
	</div>

	<div v-show="welcomePageShow" class="max-w-xl w-full space-y-12 p-10 bg-white rounded-xl z-10">
		<div class="text-center">
			<h2 class="mt-6 text-3xl font-bold text-gray-900">
				Welcome, {{ users['name'] }}
			</h2>
		</div>
	</div>
</div>
</template>