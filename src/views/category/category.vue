<template>
  <div class="category">
    <nav-bar class="cateBar"> 
      <div slot="center">商品分类</div>
    </nav-bar>
    
  <side-bar :menu="sideList" :main="mainList" @menuLoad="getSub" />
  
  </div>      
   

</template>

<script>
import BS from "better-scroll"
import { getCategory,getSubCategory } from 'network/category'

import NavBar from "components/common/navbar/NavBar"
import SideBar from "./childc/SideBar"

export default {
  name:"category",
  components:{
    SideBar,
    NavBar
  },
  data(){
    return {
      bs:null,
      sideList:[],
      mainList:[],
    }
  },
  mounted(){

  },
  created(){
    getCategory().then(v=>{
      let data= v?.data?.category?.list
      data= data !=null ? data : []
      this.sideList.push(...data)
    })

  },
  methods:{
    getSub(k){
      getSubCategory(k).then(n=>{
        let data= n?.data?.list
        data= data !==undefined ? data : [] 
        this.mainList= data
      })
    }
  },
  computed:{

  }
}
</script>
<style  scoped>
.category{
  height: 100vh;
/* overflow: hidden; */
}

.cateBar{
  background-color: var(--color-tint);
  color: #fff;
}
</style>