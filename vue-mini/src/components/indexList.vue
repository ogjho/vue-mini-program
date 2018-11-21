<template>
  <div class="hello">
    <div id="productTitle">
      <span class="blue"></span>
      <span class="titleName">{{ msg }}</span>
    </div>
    <!-- 使用 for 循环语句渲染数据 -->
    <ul id="productList">
      <li class="list" v-for="item in liData" :key="item.key">
        <router-link :to="item.link">
          <div class="photo clearfix">
            <img class="indexImg float_L" :src="item.coverImage"/>
            <div class="productsName">{{item.title}}</div>
            <div class="productsSummary">{{item.summary}}</div>
            <div class="price float_L">￥{{isDiscount ? item.discountPrice : item.marketPrice}}</div>
            <div class="iconVessel" v-if="type === 'onenter'">
              <img class="addToCart float_r" :src="item.addToCart"/>
            </div>
            <div class="iconVessel" v-else></div>
          </div>
        </router-link>
      </li>
    </ul>
    <!--<ul>
      <li v-for="item in itemsData" :key="item.key">{{item.name}}</li>
    </ul>-->
  </div>
</template>
<script>
export default {
  name: 'indexList',
  data () {
    return {
      type: '',
      isDiscount: true,
      itemsData: [
        {
          key: 0,
          name: 'aa'
        },
        {
          key: 1,
          name: 'bb'
        },
        {
          key: 2,
          name: 'cc'
        }
      ]
    }
  },
  async activated () {
    await this.isLogin()
  },
  props: {
    msg: {
      type: String
    },
    liData: {
      type: Array
    }
  },
  methods: {
    async isLogin () {
      if (!this.GLOBAL.clientData) {
        await this.GLOBAL.isLogin()
      }
      let isLogin = this.GLOBAL.clientData
      if (!isLogin) {
        this.isDiscount = false
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.titleName{
  font-size: 17px;
  color:#4e4c4d;
  display:inline-block;
  vertical-align: middle;
}
#productList{
  width:100%;
  margin:0px auto;
  background-color:#eee;
}
#productTitle{
  width:100%;
  height:45px;
  background-color: #fff;
  line-height: 45px;
}
.list{
  background-color: #fff;
  margin:5px;
  border-radius: 5px;
  padding: 15px;
  box-sizing: border-box;
}
.blue{
  width:10px;
  height:25px;
  background-color: #61BFFB;
  display:inline-block;
  vertical-align: middle;
  border-bottom-right-radius: 4px;
  border-top-right-radius: 4px;
}
.indexImg{
  width:100px;
  height: 100px;
  overflow: hidden;
  margin-right:25px;
}
.productPrice{
  width:100%;
  height:50px;
  line-height: 33px;
}
.price{
  font-size:17px;
  color:#61BFFB;
}
.productsName{
  font-size: 16px;
  line-height: 33px;
  color:#555;
}
.productsSummary{
  font-size: 14px;
  line-height: 33px;
  color:#999;
  overflow: hidden;
  text-overflow:ellipsis;
  white-space:nowrap;
}
</style>
