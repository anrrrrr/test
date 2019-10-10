<template>
  <div id="head">
      <div class="header">
          <h2>ToDoList</h2>
          <input type="text" placeholder="输入内容" class="te" v-model="txt" @keyup.enter="add()">
      </div>
  </div>
</template>

<script>
import Bus from '../Bus'
export default {
  data () {
    return {
        txt:'',
        list:[],
        flag:false
    };
  },
  methods:{
      add(){
        if (this.txt=='') {
            alert("空")
            return
        }
        this.list.push({
            'check':false,
            'txt':this.txt,
            'flag':false
        })
        //派发事件
        Bus.$emit('fine',this.list)
      }
  }
}

</script>
<style>
.header{
    width: 100%;
    height: 50px;
    background: #323232;
    display: flex;
    justify-content:center;
    align-items: center;
    color: white;
}
.te{
    width: 250px;
    height: 30px;
    margin-left: 30px;
    border-radius: 10px;

}
</style>