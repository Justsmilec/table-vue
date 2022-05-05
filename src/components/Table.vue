<template>
  <div class="hello">
    <!-- <h1>{{dataSource[0]}}</h1>
    <div v-for="(item, index) in dataSource" :key="item.id">
      {{index}}. {{item.name}}
  </div> -->

    <div class="relative overflow-x-auto shadow-md sm:rounded-lg">
      <table class="w-full text-sm text-left text-gray-500 dark:text-gray-400">
        <thead
          class="
            text-xs text-gray-700
            uppercase
            bg-gray-50
            dark:bg-gray-700 dark:text-gray-400
          "
        >
          <tr>
            <th scope="col" class="px-6 py-3">ID</th>
            <th scope="col" class="px-6 py-3">Name</th>
            <th scope="col" class="px-6 py-3">Age</th>
            <th scope="col" class="px-6 py-3">Salary</th>
            <th scope="col" class="px-6 py-3">Company</th>
            <th scope="col" class="px-6 py-3">
              <span class="sr-only">Edit</span>
            </th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item) in dataSource" :key="item.id" class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
            <th
              scope="row"
              class="
                px-6
                py-4
                font-medium
                text-gray-900
                dark:text-white
                whitespace-nowrap
              "
            >
              {{item.id}}
            </th>
            <td class="px-6 py-4">{{item.name}}</td>
            <td class="px-6 py-4">{{item.age}}</td>
            <td class="px-6 py-4">${{item.salary}}</td>
            <td class="px-6 py-4">{{item.company}}</td>

            <td class="px-6 py-4 text-right">
              <a
                href="#"
                class="
                  font-medium
                  text-blue-600
                  dark:text-blue-500
                  hover:underline
                "
                >Edit</a
              >
            </td>
          </tr>

        </tbody>
      </table>
    </div>

  </div>
</template>

<script lang="ts">
import { Options, Vue } from "vue-class-component";
import { Employee } from "../models/employee";
import { data } from "../models/data";

export default class Table extends Vue {
  msg!: string;
  dataSource: Employee[] = [];
  // data:string;
  mounted() {
    this.dataSource = data;
    console.log("----------", this.dataSource);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
