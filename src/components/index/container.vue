<template>
  <div class="m-istyle">
    <dl @mouseover="over" :class="nav.class">
      <dt>{{nav.title}}</dt>
      <dd
        v-for="(item, index) in nav.list"
        :key="index"
        :class="{active: kind == item.tab}"
        :data-type="item.tab"
      >{{item.text}}</dd>
    </dl>
    <ul class="ibody">
      <li v-for="(item,index) in list" :key="index">
        <el-card :body-style="{ padding: '0px' }" shadow="never">
          <img :src="item.image" class="image" />
          <div class="cbody">
            <div class="title" :title="item.title">{{item.title}}</div>
            <div class="sub-title" :title="item.sub_title">{{item.sub_title}}</div>
            <div class="price-info" v-if="item.rentNum && item.price_info.current_price">
              <span class="current-price-wrapper">
                <span class="price-symbol numfont">¥</span>
                <span class="current-price numfont">{{item.price_info.current_price}}</span>
              </span>
              <span class="old-price">门市价￥{{item.price_info.old_price}}</span>
              <span class="sold bottom-right-info">{{item.address}}</span>
            </div>
            <div class="price-info" v-else-if="!item.rentNum">
              <span class="current-price-wrapper">
                <span class="price-symbol numfont">¥</span>
                <span class="current-price numfont">抢光了</span>
              </span>
            </div>

            <div class="price-info" v-else>
              <span class="current-price-wrapper">
                <span class="price-symbol numfont">¥</span>
                <span class="current-price numfont">{{item.price_info.avg_price}}</span>
                <span class="units">/{{item.price_info.units}}均</span>
              </span>
            </div>
          </div>
        </el-card>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      kind: "all",
      list: [
        {
          image:
            "//p0.meituan.net/msmerchant/36cbbb3fe477d86bc7bf45714724b5f6405667.jpg@552w_312h_1e_1c",
          title: "晓本烘焙·茶本铺（东方广场店）",
          sub_title: "星座生日蛋糕1个，约6英寸，圆形",
          price_info: {
            current_price: null,
            old_price: null,
            avg_price:18,
            units:'人',
          },
          rentNum: 10,
          address: "王府井/东单"
        },
        {
          image:
            "//p1.meituan.net/msmerchant/edabcb17c64d979c2bebf568dab11598116805.jpg@552w_312h_1e_1c",
          title: "中央电视塔空中观景旋转餐厅",
          sub_title: "午餐+观光",
          price_info: {
            current_price: 248,
            old_price: 268,
             avg_price:null,
            units:null,
          },
            rentNum: 100,
          address: "航天桥"
        }
      ]
    };
  },
  props: ["nav"],
  methods: {
    over(e) {
      let dom = e.target;
      let tagName = dom.tagName.toLowerCase();
      if (tagName != "dd") {
        return false;
      }
      this.kind = dom.getAttribute("data-type");
      console.log(this.kind);
    }
  }
};
</script>

<style lang="scss">
@import "@/assets/css/index/artistic.scss";
</style>


