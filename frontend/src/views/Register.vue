<script setup>
import { ref } from "vue"
import api from "@/services/api"
import { useRouter } from "vue-router"

const router = useRouter()

const email = ref("")
const password = ref("")
const loading = ref(false)
const error = ref("")

const submit = async () => {
  error.value = ""
  loading.value = true

  try {
    await api.post("/auth/register", {
      email: email.value,
      password: password.value,
    })

    router.push("/login")
  } catch (err) {
    error.value =
      err.response?.data?.detail || "Register gagal"
  } finally {
    loading.value = false
  }
}
</script>

<template>
  <div class="min-h-screen flex items-center justify-center bg-gray-100">
    <form
      @submit.prevent="submit"
      class="w-96 bg-white p-6 rounded shadow space-y-4"
    >
      <h2 class="text-xl font-semibold text-center">
        Register
      </h2>

      <div v-if="error" class="text-red-500 text-sm">
        {{ error }}
      </div>

      <input
        v-model="email"
        type="email"
        placeholder="Email"
        class="w-full border px-3 py-2 rounded"
        required
      />

      <input
        v-model="password"
        type="password"
        placeholder="Password"
        class="w-full border px-3 py-2 rounded"
        required
      />

      <button
        type="submit"
        :disabled="loading"
        class="w-full bg-blue-600 text-white py-2 rounded hover:bg-blue-700"
      >
        {{ loading ? "Loading..." : "Register" }}
      </button>
    </form>
  </div>
</template>
