<template>
  <div class="vuex-demo">
    <!-- 头部 -->
    <Header :title="name"></Header>

    <main class="goods-list">
      <Scroll>
        <ul class="good-list">
          <li v-for="(good,index) in goodsApi.goods" :key="good.id" class="goodLi">
            <div class="left-img">
              <img :src="good.listPicUrl" alt="">
            </div>
            <div class="right-description">
              <p class="good-name">{{good.name}}</p>
              <p class="good-des">{{good.simpleDesc}}</p>
              <div class="num-click">
                <span class="good-price">￥{{good.retailPrice}}</span>
                <div class="click-area">
                  <span class="less click-icon" :class="{'goods-disable': good.pieceNum == 0}" @click="onReduce(index)">-</span>
                  <input class="good-num" type="text" v-model="good.pieceNum" readonly="readonly" />
                  <span class="more click-icon" @click="onAdd(index)">+</span>
                </div>
              </div>
            </div>
          </li>
        </ul>
      </Scroll>
    </main>

    <footer>
      <div class="foot-area money"><span class="money-des">合计:</span>￥{{ tatolPrice || 0 }}</div>
      <div class="foot-area peisong">配送费:￥{{goodsApi.deliveryPrice}}</div>
      <div class="foot-area goods-submit" :class="{'goods-submit-active': tatolPrice >= parseFloat(goodsApi.minPrice) }">
        {{ cartStatus }}({{ tatolNum }}件)
      </div>
    </footer>
  </div>
</template>

<script>
    import {mapState,mapGetters,mapMutations} from "vuex"//通过辅助函数引用store中的定义的方法和数据
    import Scroll from "@/components/Scroll.vue"
    import Header from "@/components/Header.vue"
    export default {
        name: "Goods",
        components: {
          Header,
          Scroll,
        },
        computed: {
          ...mapState(["name","goodsApi"]),
          ...mapGetters(['tatolPrice','tatolNum']),
          cartStatus() {
            let cartStatusInfo = '';
            if(this.tatolPrice == 0){
              cartStatusInfo = `${this.goodsApi.minPrice}元起送`
            }else if(parseFloat(this.tatolPrice) < this.goodsApi.minPrice && parseFloat(this.tatolPrice) > 0){
              cartStatusInfo = `还差${this.goodsApi.minPrice - this.tatolPrice}元起送`;
            }else{
              cartStatusInfo = '去买单'
            }
            return cartStatusInfo
          }
        },
        methods: {
          ...mapMutations(['goodsReduce','goodsAdd']),
            onReduce(index){
              this.goodsReduce(index);
            },
            onAdd(index){
              this.goodsAdd(index);
            }
        }
    }
</script>

<style lang="stylus">
  @import "../assets/Goods.styl"
</style>
