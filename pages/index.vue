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
          <template v-if="jankenStatus">
            {{startCountDownDefault}}
          </template>
          <template v-else>
            じゃんけん
          </template>
        </div>
        <div class="content__action">
          <template v-if="jankenStatus">
            <div class="actions">
               <button class="btn normal" @click="start">ぐー</button>
               <button class="btn normal" @click="start">ちょき</button>
               <button class="btn normal" @click="start">ぱー</button>
            </div>
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
    jankenStatus: false,
    startCountDownDefault: 3
  }),

  methods: {
    start(e) {
      this.jankenStatus = true;
      setInterval( () =>{
        if(0 < this.startCountDownDefault) {
          this.startCountDownDefault--;
        }
      }, 1000);
    },
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
  font-size: 5rem;
  position: absolute;
  top: -150px;
  left: 0;
  right: 0;
  bottom: 0;
}

.container .content .content__action {
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
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
.btn.normal {
  color: #696969;
  background-color: #dfdfdf
}
.btn.normal:hover {
  color: #fff;
  background-color: #696969;
}

</style>
