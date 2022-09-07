<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js + TypeScript App" />
  </div>
</template>
<script lang="ts" setup>
import { onMounted } from 'vue';
import DataService from '@/services/DataService';
import IResponseData from '@/types/ResponseData';
import HelloWorld from '@/components/HelloWorld.vue'; // @ is an alias to /src
onMounted(() => {
  DataService.getAll()
    .then((response: IResponseData) => {
      console.log(response);
    })
    .catch((e: Error) => console.log(e));
});
</script>
