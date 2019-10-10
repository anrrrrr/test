<template>
  <div id="can" v-show="fexd">

    <h1>修改数据</h1>
    <input type="text" @keyup.esc="save(index)">
  </div>
</template>

<script>     
import Bus from '../Bus'
export default {
  data () {
    return {
      fexd:false
    };
  },
  created(){
    Bus.$on("end",(v)=>{
      this.fexd=v;
    })
  },
  methods:{
    save(index){
      this.list[index].uiu=false;
    }
  }
}

</script>
<style>
#can{
  width: 300px;
  height: 200px;
  background: gray;
  text-align: center;
  color: gainsboro;
  margin-left: 400px;
  position: absolute;
}
</style>