<script setup>
import api from "../services/api"
import { ref } from "vue"

const email = ref("")
const password = ref("")

const submit = async () => {
  const res = await api.post("/auth/login", {
    email: email.value,
    password: password.value
  })
  localStorage.setItem("token", res.data.access_token)
  alert("Login success")
}
</script>

<template>
  <div class="min-h-screen flex items-center justify-center">
    <form @submit.prevent="submit" class="w-80 space-y-4">
      <h2 class="text-xl font-semibold">Login</h2>
      <input v-model="email" class="input" placeholder="Email" />
      <input v-model="password" type="password" class="input" placeholder="Password" />
      <button class="btn">Login</button>
    </form>
  </div>
</template>
