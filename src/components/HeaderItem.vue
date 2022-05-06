<template>
      <th @click="$emit('sort',title)" scope="col" class="px-6 py-3" >
          <div class="flex flex-row ml-50">
                <span>{{title}}</span>
                <span>
                    <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 32 32" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" :d="svgImage"></path></svg>
                </span>
          </div>
    </th>

</template>

<script lang="ts">
    import { Options, Vue } from "vue-class-component";


    @Options({
        props:{
            title: String,
        }
    })
    export default class HeaderItem extends Vue {

        title!: string;
        
        /*
        if false is desc else asc
        */
        ascSort: any = undefined;
        sortCount: any = 0;
        // descSort: any = false;

        svgSortingImage:any[] = [
            "M9 3v2m6-2v2M9 19v2m6-2v2M5 9H3m2 6H3m18-6h-2m2 6h-2M7 19h10a2 2 0 002-2V7a2 2 0 00-2-2H7a2 2 0 00-2 2v10a2 2 0 002 2zM9 9h6v6H9V9z",
            "M19 14l-7 7m0 0l-7-7m7 7V3",
            "M5 10l7-7m0 0l7 7m-7-7v18"
        ];
        svgImage: string = this.svgSortingImage[this.sortCount];


        sortMethod(column: any) {            
            if( this.ascSort == undefined ){
                this.ascSort = true;
                this.sortCount = 2;
            } else{
                this.ascSort = !this.ascSort;
                this.sortCount = this.ascSort ? 2 : 1;    
            }
            this.svgImage = this.svgSortingImage[this.sortCount];

        }
        // data:string;
    //     mounted() {
    // }


    }
</script>