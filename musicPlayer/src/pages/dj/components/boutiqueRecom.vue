<!--
 * @Author: 李浩栋
 * @Begin: 2019-10-11 13:11:46
 * @Update: 2019-12-10 18:59:09
 * @Update log: 更新日志
 -->
<template>
  <div class="wrapper">
    <div class="title">
      <h1 class="text">精品推荐</h1>
      <span class="smallTag" @click="goPage">全部精品</span>
    </div>
    <div class="img-col">
      <img-card
        v-for="(item, index) in boutiqueRecomList"
        :key="index"
        type="dj"
        :name="item.name"
        :imgUrl="item.picUrl"
        :dec="item.rcmdText"
        :ridId="item.id"
      ></img-card>
    </div>
  </div>
</template>

<script>
import api from 'api'
import imgCard from 'base/imgCard'

export default {
  name: '',
  data () {
    return {
      boutiqueRecomList: []
    }
  },
  created () {
    this._getBoutiqueRecom()
  },
  methods: {
    _getBoutiqueRecom () {
      api.boutiqueRecomFn()
        .then(res => {
          const data = res.data
          if (data.code === 200) {
            this.boutiqueRecomList = data.data.list
          }
        })
    },
    goPage () {
      this.$router.push('/pay_fine')
    }
  },
  components: {
    imgCard
  }
}
</script>

<style lang='less' scoped>
@import url("~styles/global.less");
.wrapper {
  margin-top: 0.5rem;
  .title {
    .flex-between();
    align-items: center;
    .text {
      font-weight: 700;
    }
  }
  .img-col {
    .flex-between();
    flex-wrap: wrap;
  }
}
</style>
