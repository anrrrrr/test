<template>
  <div id="list">

      <h2>正在进行{{list.length-con2}}</h2>
      <ol>
          <li v-for="(item,index) in list" :key="index" v-show="!item.done">
              <input type="checkbox" class="put" v-model="item.done">
              <p class="nei" @click="uiu">{{item.txt}}</p>
              <button class="shan" @click="del(index)">删除</button>
          </li>
      </ol>

      <h2>已经完成{{con2}}</h2>
      <ol>
          <li v-for="(item,index) in list" :key="index" v-show="item.done">
              <input type="checkbox" class="put" v-model="item.done">
              <p class="nei">{{item.txt}}</p>
              <button class="shan" @click="del(index)">删除</button>
          </li>
      </ol>

        <!-- 导入can can里有编辑  -->
      <Can></Can>

  </div>
</template>

<script>
import Can from './can'
import Bus from '../Bus'
export default {
  data () {
    return {
        list:[],
        gu:false
    };
  },
  components:{
      Can
  },
  created(){//接受
      Bus.$on('fine',(data)=>{
          console.log(data)
          this.list=data;
      })
  },
  methods:{
      del(index){//删除
        this.list.splice(index,1)
      },
      uiu(){//编辑框
          Bus.$emit("end",this.gu=!this.gu)
      }
  },
  computed:{
      con1(){//添加进来的数据1
          let n=0;
        for(let i=0;i<this.list.length;i++){
            if(this.list[i].done==false){
                n++;
            }
        }
        return n;
      },
      con2(){
          let n=0;
        for(let i=0;i<this.list.length;i++){
            if(this.list[i].done==true){
            n++;
            }
        }
        return n;
      }
  },
  watch:{//监听
    list:{
        handler(){
            var obj={
                'list':this.list
            }
            var str=JSON.stringify(obj)
            localStorage.setItem('zhi',str)
        },
        deep:true
    }
  },
  mounted(){
      var str=localStorage.getItem('zhi');
      if (str) {
          let obj=JSON.parse(str);
          this.list=obj.list
      }else{
          this.list=[]
      }
  }
}

</script>
<style>
#list{
    width: 100%;
    height: 600px;
    background: #CDCDCD;
}
ol{
    list-style: none;
}
li{
    width: 100%;
    height: 30px;
    background: white;
    margin-top: 15px;
    display: flex;
    align-items: center;
}
.put{
    width: 20px;
    height: 20px;
    margin-left: 20px;
}
.shan{
    margin-left: 300px;
}
.nei{
    margin-left: 100px;
}
</style>