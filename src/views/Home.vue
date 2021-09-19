<template>
  {{ message }}
</template>

<script lang="ts">
import {onMounted, ref} from 'vue';
import {useStore} from "vuex";

export default {
  name: "Home",
  setup() {
    //tidak memiliki cookie login
    const message = ref('Kamu tidak Login');
    const store = useStore();

    onMounted(async () => {
      try {
        //mengambil data user apakah ada pada jwt/cookie
        const response = await fetch('http://localhost:8000/api/user', {
          headers: {'Content-Type': 'application/json'},
          credentials: 'include'
        });

        const content = await response.json();

        message.value = `Selamat Datang  ${content.nama}`;

        await store.dispatch('setAuth', true);
      } catch (e) {
        await store.dispatch('setAuth', false);
      }
    });

    return {
      message
    }
  }
}
</script>
