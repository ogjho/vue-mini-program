<template>
  <div class="hello">
    <!-- <h1>{{ msg }}</h1> -->
    <banner :bannerData="bannerData"></banner>
    <List :msg="test2" :liData="liData" style="padding-bottom: 50px;"></List>

    <!-- 使用 router-link 组件来导航. -->
    <!-- 通过传入 `to` 属性指定链接. -->
    <!-- <router-link> 默认会被渲染成一个 `<a>` 标签 -->
    <onenterMenu :selected="selected"></onenterMenu>
  </div>
</template>

<script>
import banner from '../common/banner.vue'
import List from '../common/indexList.vue'
import onenterMenu from '../common/onenterMenu.vue'
import axios from '../../router/ajaxModel'
export default {
  components: {banner, List, onenterMenu},
  data () {
    return {
      selected: 'home',
      type: '',
      msg: 'Welcome to Your Vue.js App',
      test: 'hello test',
      test2: '产品展示',
      liData: [
        {
          key: '1',
          contentId: 10001,
          name: '多功能水槽',
          price: '￥3999.99',
          production: './static/images/production1.png',
          addToCart: './static/images/addToCart.png',
          link: '/detail/10001'
        },
        {
          key: '2',
          contentId: 10002,
          name: '多功能水槽',
          price: '￥3999.99',
          production: './static/images/production1.png',
          addToCart: './static/images/addToCart.png',
          link: '/detail/10002'
        },
        {
          key: '3',
          contentId: 10003,
          name: '多功能水槽',
          price: '￥3999.99',
          production: './static/images/production1.png',
          addToCart: './static/images/addToCart.png',
          link: '/detail/10003'
        }
      ],
      bannerData: []
    }
  },
  created () {
    console.log(this.$route.query)
    this.type = this.$route.query.type
    this.fetchBannerData()
    this.fetchProductData()
  },
  methods: {
    fetchProductData: async function () {
      let data = await axios.ajaxGet('/product/all', {
        pageIndex: 1
      })
      if (data.code !== 0) {
        this.$message.error(data.msg)
        return
      }
      let result = data.data.data
      for (let i = 0; i < result.length; i++) {
        result[i].coverImage = this.URL + result[i].coverImage
        result[i].key = result[i].contentId
        result[i].link = '/detail/' + result[i].contentId
      }
      this.liData = result
      console.log(result)
    },
    fetchBannerData: async function () {
      let data = await axios.ajaxGet('/scroll/get')
      if (data.code !== 0) {
        this.$message.error(data.msg)
        return
      }
      let result = data.data.data
      for (let i = 0; i < result.length; i++) {
        result[i].coverImage = this.URL + result[i].coverImage
        result[i].key = result[i].contentId
        result[i].link = '/detail/' + result[i].contentId
      }
      this.bannerData = result
    }
  }
}
</script>
