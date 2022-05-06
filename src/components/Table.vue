<template>
  <div  class="hello">
    <!-- <h1>{{dataSource[0]}}</h1>
    <div v-for="(item, index) in dataSource" :key="item.id">
      {{index}}. {{item.name}}
  </div> -->

    <input @input="onFilterCompany" v-model="filter" placeholder="Search Company">
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

            <HeaderItem title="ID"/>
            <HeaderItem ref="headeritemName" @sort="sortMethod" @click="$refs.headeritemName.sortMethod()" title="Name"/>
            <HeaderItem title="Age"/>
            <HeaderItem ref="headeritemID" @sort="sortMethod" @click="$refs.headeritemID.sortMethod()" title="Salary"/>
            <HeaderItem title="Company"/>


            <th scope="col" class="px-6 py-3">
              <span class="sr-only">Edit</span>
            </th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item) in !isFilterActive ? displayingDataSource : filteredDataSource" :key="item.id" class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
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

      <VueTailwindPagination
        ref="pagin"
        :current="currentPage"
        :total="total"
        :per-page="perPage"
        @page-changed="currentPage = $event"

       />

    </div>


  

  </div>
</template>


<script lang="ts">
import { Options, Vue } from "vue-class-component";
import { Employee, HeaderItemElement } from "../models/employee";
import { data } from "../models/data";
import HeaderItem from "./HeaderItem.vue";
import VueTailwindPagination  from '@ocrv/vue-tailwind-pagination'

@Options({
  components: {
    HeaderItem,
    VueTailwindPagination,
  },
})


export default class Table extends Vue {
  msg!: string;
  dataSource: Employee[] = [];
  displayingDataSource: Employee[] = [];
  filteredDataSource: Employee[] = [];
  isFilterActive = false;
  actuallyClickedHeader = "";
  isActuallyForAsc = false;
  isFirstTime = true;

  currentPage: any = 1;
  perPage:any =  5;
  total:any =  20;
  filter:any =  '';

  headerItems: HeaderItemElement[] = [
    {
      headerTitle: "ID",
      headername: "id",
    },
    {
      headerTitle: "Name",
      headername: "name",

    },
    {
      headerTitle: "Age",
      headername: "age",
    },
    {
      headerTitle: "Salary",
      headername: "salary",
    },
    {
      headerTitle: "Company",
      headername: "company",
    },
  ]

  // data:string;
  mounted() {
    this.dataSource = data;
    this.displayingDataSource = this.dataSource;
  }


    
  onFilterCompany = () =>{
    console.log(this.filter.length)
    if(this.filter.length > 2){
      this.isFilterActive = true;
      this.filteredDataSource = this.displayingDataSource.filter(item => item.company.includes(this.filter))

    } else{
      this.isFilterActive = false;
      this.filteredDataSource = this.displayingDataSource;
      console.log(this.displayingDataSource);
      
    }

  }

  sortMethod = (item: string) => {

    
    let clickedHeader = JSON.parse(JSON.stringify(this.headerItems.find(item_ => 
      item_.headerTitle == item
    ))) 
    // debugger
    if(clickedHeader){      
      this.isFirstTime ?  this.actuallyClickedHeader = clickedHeader.headername : null;
      this.isFirstTime = false;
      this.isActuallyForAsc = !this.isActuallyForAsc;
      this.actuallyClickedHeader === clickedHeader.headername ? null : (this.isActuallyForAsc = false);
      this.displayingDataSource  = JSON.parse(JSON.stringify(this.sortColumn(clickedHeader.headername,this.filteredDataSource)));
      this.actuallyClickedHeader = clickedHeader.headername;

    }
  }

  sortColumn = (columnTitle: string,filteredList:Employee[]) => {

    this.displayingDataSource = this.isFilterActive ? filteredList :  this.dataSource;
        if(this.isActuallyForAsc){
          return this.displayingDataSource.sort( function(a:any,b:any) {
              if (a[columnTitle] < b[columnTitle]) {
                  return -1;
                }
                if (a[columnTitle] > b[columnTitle]) {
                  return 1;
                }
                return 0;
            })
        } else{
          return this.displayingDataSource.sort( function(a:any,b:any) {
              if (a[columnTitle] > b[columnTitle]) {
                  return -1;
                }
                if (a[columnTitle] < b[columnTitle]) {
                  return 1;
                }
                return 0;
            })
        }

    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
