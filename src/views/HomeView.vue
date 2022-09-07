<template>
  <button @click="alertMessage">+</button>
  <div v-if="loading">loading....</div>
  <div v-else>
    <table>
      <thead>
        <tr>
          <td>name</td>
          <td>gender</td>
          <td>mass</td>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(people, index) in peoples.results" :key="index">
          <td>{{ people.name }}</td>
          <td>{{ people.gender }}</td>
          <td>{{ people.mass }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script lang="ts">
import { onMounted, ref, defineComponent } from 'vue';
import DataService from '@/services/DataService';
import IResponseData from '@/types/ResponseData';
import IPersonsList from '@/types/PersonsList';

export default defineComponent({
  setup() {
    const loading = ref<boolean>(true);
    const peoples = ref({} as IPersonsList);
    onMounted(() => {
      DataService.getAll()
        .then((response: IResponseData) => {
          peoples.value = response.data;
        })
        .catch((e: Error) => console.log(e))
        .finally(() => (loading.value = false));
    });
    function alertMessage() {
      alert('****');
    }
    return {
      loading,
      peoples,
      alertMessage,
    };
  },
});
</script>
