<template>
  <div class="container">
    <div class="header">
      <div class="header__wrap">
        <div class="title">
          <nuxt-link to="/">{{base.siteTitle}}</nuxt-link>
        </div>
        <div class="navi">
        </div>
      </div>
    </div>

    <div class="content">
      <div class="content__wrap">
        <div class="content__text">
          じゃんけん
        </div>
        <div class="content__action">
          <template v-if="jankenStatus">
            a
          </template>
          <template v-else>
            <button class="btn success" @click="start">開始</button>
          </template>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
export default {
  components: {},

  data: () => ({
    base: {
      siteTitle: '勝まくりジャンケンゲーム',
      version:   1.0
    },
    jankenStatus: false
  }),

  methods: {
    start(e) {
      this.jankenStatus = true;
    }
  },

}
</script>

<style>
.container {

}

.container .header {
  background-color: #99E5FF;
  box-shadow: 0 0 3px #65D8FF;
  line-height: 3;
  border-bottom: 1px #ddd solid;
}
.header .header__wrap {
  display: flex;
  justify-content: space-between;
}
.header .header__wrap .title {
  text-shadow: 0 0 1px #ccc;
  font-weight: bold;
  padding-left: 10px;
}
.header .header__wrap .title a {
  color: #696969;
  text-decoration: none;
}
.header .header__wrap .title a:hover {
  color: #A9A9A9;
  text-decoration: underline;
}

.container .content {
  width: 100%;
}

.container .content .content__wrap {
  width: 95%;
  margin: 0 auto;
  text-align: center;
  position: relative;
    top: 200px;
}

.container .content .content__text {
  font-size: 52px;
}

.btn {
  padding: 10px;
  font-size: 18px;
  width: 200px;
  box-shadow: 0 0 1px #ddd;
  border-radius: 10px;
}
.btn:hover {
  opacity: 0.8;
}
.btn.success {
  color: #fff;
  background-color: #9ACD32;
}

</style>
