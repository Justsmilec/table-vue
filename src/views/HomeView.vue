<template>
  <div class="home">
    <Table msg="This is my Table"/>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import Table from '@/components/Table.vue'; // @ is an alias to /src

@Options({
  components: {
    Table,
  },
})
export default class HomeView extends Vue {}
</script>
