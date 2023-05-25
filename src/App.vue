<template>
 <div class="fullscreen">

 <SelectComponenet/>
  </div>
</template>

<script>
import SelectComponenet from "./components/SelectComponent.vue"
export default{

  data(){
return{

}
  },
  components:{
    SelectComponenet,
  },
  methods: {
   
  }
};
</script>

<style lang="less">
    body, html {
      margin: 0;
      padding: 0;
    }
    
    .fullscreen {
      width: 100vw;
      height: 100vh;
      background-color: #f2f2f2;
      padding: 5px;
      // display: flex;
      // align-items: center;
      // justify-content: center;
      // text-align: center;
      font-size: 24px;
    }
</style>
