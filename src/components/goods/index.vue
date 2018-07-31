<template>
    <div class="goods_detail">
        <header class="top_bar">
            <a @click="goBack" class="icon_back"></a>
            <!-- <a onclick="window.history.go(-1)" class="icon_back"></a> -->
            <h3 class="top_bar_name">商品详情</h3>
            <a href="#" class="icon_menu"></a> 
        </header>
        <main class="detail_box">
            <section class="banner_box">
                <ul class="banner_child_box">
                    <li class="banner_item" :key="item.image_url" v-for="item in goodsImages">
                        <img :src="item.image_url" alt="" class="banner_pic">
                    </li>
                
                </ul>
                <div class="banner_count">
                    <em id="slide-nub" class="fz18">{{ num+1 }}</em>
                    <em class="nub-bg">/</em>
                    <em id="slide-sum" class="fz12">{{ goodsImages.length }}</em>
                </div>

            </section>
            <section class="product_info clearfix">
                <div class="product_left">
                    <p class="p_name">{{goodsData[0] ? goodsData[0].product_name : ''}}</p>
                    <div class="product_pric">
                        <span>￥</span>
                        <span class="rel_price">{{goodsData[0] ? goodsData[0].product_price : ''}}</span>
                        <span>.00</span>
                    </div>
                    <div class="product_right">
                        降价通知
                    </div>
                </div>

            </section>
            <section class="product_intro">
                <p class="pro_det">
                    {{goodsData[0] ? goodsData[0].product_detail : ''}}
                </p>
           </section>
          
        </main>
        <footer class="cart_d_footer">
            <div class="m">
                <ul class="m_box">
                    <li class="m_item">
                        <a href="" class="m_item_link">
                            <em class="m_item_pic"></em>
                            <span class="m_item_name">卖家</span>
                        </a>
                        <a href="" class="m_item_link">
                            <em class="m_item_pic two"></em>
                            <span class="m_item_name">关注</span>
                        </a>
                        <a href="" class="m_item_link">
                            <em class="m_item_pic three"></em>
                            <span class="m_item_name">购物车</span>
                        </a>
                    </li>
                </ul>
                <div class="btn_box clearfix" >
                    <a href="#" class="buy_now" @click="addToCart()">加入购物车</a>
                    <a href="#" class="buybuy">立即购买</a>
                </div>
            </div>
        </footer>
    </div>
</template>
<script>
import { mapGetters, mapActions } from "vuex";
export default {
  mounted() {
    this.fetchData(this.$route.params.id);
    this.$store.dispatch("hideNav");
  },
  destroyed() {
    //销毁完成状态
    this.$store.dispatch("showNav");
  },
  data() {
    return {
      num:0,
      cateGoodsAllData: [],
      goodsImages: [],
      goodsData: []
    };
  },
  watch: {
    $route(to) {
      //console.log(to);
      var reg = /detail\/\d+/;
      if (reg.test(to.path)) {
        var categotyId = this.$route.params.id || 0;
        this.fetchData(categotyId);
      }
    }
  },
  methods: {
    goBack() {
      //    window.history.back(-1);
      this.$router.back("");
    },
    autoplay(){
        this.num++;
        if(this.num == this.goodsImages.length){
            this.num = 0;
        }
    },
    play(){
        setInterval(() => {
            this.autoplay();
        },3000)
    },
    async fetchData(id) {
      try {
        var _this = this;
        let result = await _this.$http.get("/detail", {
          params: {
            mId: id
          }
        });
        if (result.data && result.data.length) {
          const goodsDetail = result.data;
          _this.goodsImages = goodsDetail[0];
          _this.goodsData = goodsDetail[1];
          console.log(_this.goodsImages);
          _this.play();
        }
      } catch (error) {
        console.log(error);
      }

      // _this.$http.get('/detail',{
      //     params: {
      //         mId: id
      //     }
      // }).then((res)=>{
      //     console.log(res.data);
      //     _this.goodsImages = res.data[0];
      //     _this.goodsData = res.data[1];

      // },(err)=>{
      //     console.log(err);
      // })
    },
    //加入购物车
    addToCart() {
      //序列化
      let data = JSON.parse(JSON.stringify(this.goodsData[0]));
      console.log(data);
      data.goods_num = 1;
      this.$store.dispatch("cartAdd", data); //将data存入store
      this.$router.push("/cart");
    }
  }
};
</script>
<style>
@import "../../assets/css/detail.css";
</style>