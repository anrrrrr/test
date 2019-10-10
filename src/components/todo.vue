<template>
  <div id="todo">
      <Head></Head>
      <List></List>
      
  </div>
</template>

<script>
// 导入head head是头部 里面有input框
import Head from '@/components/head'
// 导入list list里面有添加进来的内容
import List from '@/components/list'

export default {
  data () {
    return {
    };
  },
  components:{
      Head,
      List
  }
}

</script>
<style>

</style>