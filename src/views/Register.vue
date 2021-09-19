<template>
  <form @submit.prevent="submit">
    <h1 class="h3 mb-3 fw-normal">Register</h1>

    <input v-model="data.nama" class="form-control" placeholder="Nama" required>

    <input v-model="data.email" type="email" class="form-control" placeholder="Email" required>

    <input v-model="data.password" type="password" class="form-control" placeholder="Password" required>

    <button class="w-100 btn btn-lg btn-primary" type="submit">Submit</button>
  </form>
</template>

<script lang="ts">
import {reactive} from 'vue';
import {useRouter} from "vue-router";

export default {
  name: "Register",
  setup() {
    const data = reactive({
      nama: '',
      email: '',
      password: ''
    });
    const router = useRouter();
    //mengirim data form ke backend dengan method post
    const submit = async () => {
      await fetch('http://localhost:8000/api/register', {
        method: 'POST',
        headers: {'Content-Type': 'application/json'},
        body: JSON.stringify(data)
      });

      await router.push('/login');
    }

    return {
      data,
      submit
    }
  }
}
</script>