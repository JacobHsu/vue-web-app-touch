<template>
  <div class="hello">
    <h3>{{ msg }}</h3>
    <delete-slider v-for="(list, index) in dataList" :key="index" @deleteLine="deleteLine(index, list.id)">
      <div class="li-img" slot="img"><img :src="list.img" alt=""></div>
      <h3 class="li-title" slot="title">{{list.title}}</h3>
      <p class="li-price" slot="price">{{list.price}}</p>
    </delete-slider> 
  </div>
</template>

<script>
import deleteSlider from '@/components/deleteTemplate.vue' 
export default {
  name: 'HelloWorld',
  components: {
    deleteSlider
  },
  data () {
    return {
      msg: 'Tips：請在移動端設備上訪問或者瀏覽器上使用調試模式切換到移動端開發進行預覽',
      dataList: [
        {
          id: 1,
          img: 'static/a1.jpg',
          title: '法國專櫃2019夏季新款修身顯瘦氣質包臀短裙鏤空蕾絲性感連衣裙子',
          price: '399.00'
        },
        {
          id: 2,
          img: 'static/a2.jpg',
          title: 'VERAMOON 亮片印花短袖連衣裙女夏甜美露背性感泡泡袖修身短裙',
          price: '689.00'
        },
        {
          id: 3,
          img: 'static/a3.jpg',
          title: 'famous 仙氣木耳邊紫色小碎花短裙a字雪紡連衣裙女',
          price: '199.00'
        },
        {
          id: 4,
          img: 'static/a4.jpg',
          title: '灰灰定製 2019春夏新款小香風粗花呢連衣裙女法式名媛復古短裙M家',
          price: '298.00'
        }
      ]
    }
  },
  methods:{
    deleteLine (index, id){
      console.log(id);
      
      this.dataList.splice(index, 1)
    }      
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.li-img{
  float: left; 
  width: 100px; 
  height: 100px; 
  margin: 10px; 
  overflow: hidden;
}
.li-title{
  font-size: 18px; 
  height: 50px; 
  overflow: hidden;
}
.li-price{
  height: 26px; 
  color: #f60;
}
</style>
