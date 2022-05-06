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
            <!-- <th @click="myclick" scope="col" class="px-6 py-3">ID</th> -->
            <!-- <th scope="col" class="px-6 py-3">
              Name <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 3v2m6-2v2M9 19v2m6-2v2M5 9H3m2 6H3m18-6h-2m2 6h-2M7 19h10a2 2 0 002-2V7a2 2 0 00-2-2H7a2 2 0 00-2 2v10a2 2 0 002 2zM9 9h6v6H9V9z"></path></svg>
            </th> -->
            <HeaderItem title="ID"/>
            <HeaderItem @sort="sortMethod" @click.prevent="sortMethod() ref="post" title="Name"/>
            <!-- <th scope="col" class="px-6 py-3">Age</th> -->
            <HeaderItem title="Age"/>
            <HeaderItem @sort="sortMethod" title="Salary"/>
            <HeaderItem title="Company"/>
<!-- 
            <th scope="col" class="px-6 py-3">Salary</th>
            <th scope="col" class="px-6 py-3">Company</th> -->
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
import HeaderItem from "./HeaderItem.vue";

@Options({
  components: {
    HeaderItem,
  },
})

export default class Table extends Vue {
  msg!: string;
  dataSource: Employee[] = [];

  // data:string;
  mounted() {
    this.dataSource = data;
  }

  myclick = () =>{
    console.log("----------");
    this.dataSource = [];
    
  }

  sortMethod = (item: string) => {
    console.log("-----------asdasd", item);
    
  }


  toggleDetails () {
    this.$refs.post.toggleDetails()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
