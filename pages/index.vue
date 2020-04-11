<template>
  <div class="container">
    <div class="header">
      <div class="header__wrap">
        <div class="title">
          <nuxt-link to="/">{{base.siteTitle}} v{{base.version}}</nuxt-link>
        </div>
        <div class="navi">
        </div>
      </div>
    </div>

    <div class="content">
      <div class="content__wrap">
        <div class="content__text">
          <template v-if="jankenStatus">
            <template v-if="gameStartStatus">
              <div class="img">
                <img :src="jankenImages[cpuSelectJankenActionNumber]" width="260" />
              </div>
            </template>
            <template v-else>
              {{startCountDownDefault}}
            </template>
          </template>
          <template v-else>
            じゃんけん
          </template>
        </div>
        <div class="content__action">
          <template v-if="jankenStatus">
            <div class="actions">
              <template v-for=" (junken, index) in jankenAction">
                <button class="btn normal" @click="action" :data-no="index" :class="{ active: selectJanken[index]}" :key="index">{{junken}}</button>
              </template>
            </div>
          </template>
          <template v-else>
            <button class="btn success" @click="start">開始</button>
          </template>
        </div>
        <div class="content__message" v-show="gameStartStatus">
          <div v-html="gameMessage"></div>
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
      version:   '1.0'
    },
    jankenStatus: false,
    gameStartStatus: false,
    cpuSelectJankenActionNumber: 3,
    plauerSelectJankenActionNumber: -1,
    startCountDownDefault: 3,
    selectJanken: [false,false,false],
    jankenAction: ["ぐー", "ちょき", "ぱー"],
    jankenImages: ["/guu.jpg", "/choki.jpg", "/pa.jpg", "/syori.jpg"],
    gameMessage: null
  }),

  watch: {
    startCountDownDefault(value) {
      let judge;
      if(value < 1) {
        this.gameStartStatus = true;
        this.jankenInputSystemActionValue();


        judge = this.jankenConditions(
          this.plauerSelectJankenActionNumber,
          this.cpuSelectJankenActionNumber
        );

        if(judge.indexOf("完全勝利") === -1) {
          this.gameMessage = `
          コンピュータは、${this.jankenAction[this.cpuSelectJankenActionNumber]} を出しました。<br />
          ${judge} です。
          `;
        } else {
          this.gameMessage = `
          おめでとうございます。何も選択しなかったので、${judge} です。
          `;
        }

      }
    }
  },

  methods: {
    start(e) {
      this.jankenStatus = true;
      setInterval( () =>{
        if(0 < this.startCountDownDefault) {
          this.startCountDownDefault--;
        }
      }, 1000);
    },
    action(e) {
      this.selectJanken.forEach( (key, index) => {
        this.selectJanken[index] = Number(e.target.dataset.no) == index ? true : false;
      });
      this.selectJanken.splice();

      this.plauerSelectJankenActionNumber = Number(e.target.dataset.no);
    },
    jankenInputSystemActionValue() {
      switch(this.plauerSelectJankenActionNumber) {
        case 0:
          this.cpuSelectJankenActionNumber = 2;
          break;
        case 1:
          this.cpuSelectJankenActionNumber = 0;
          break;
        case 2:
          this.cpuSelectJankenActionNumber = 1;
          break;
      }

    },
    jankenConditions(player, cpu) {
      if(player == -1) return "あなたは完全勝利";
      if(player == cpu){
        return "引き分け";
      }
      if(player == 0 && cpu == 1 || player == 1 && cpu == 2 || player == 2 && cpu == 0) {
        return "あなたの勝ち";
      } else {
        return "あなたの負け";
      }
    }
  },
}
</script>

<style>
.container {
  margin: 0px;
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
    top: 300px;
}

.container .content .content__text {
  font-size: 5rem;
  position: absolute;
  top: -150px;
  left: 0;
  right: 0;
  bottom: 0;
}

.container .content .content__text .img {
  margin-top: 10px;
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

.container .content .content__message {
  position: absolute;
  left: 0;
  right: 0;
  top: 100px;
}

.btn {
  padding: 10px;
  font-size: 18px;
  width: 200px;
  box-shadow: 0 0 1px #ddd;
  border-radius: 10px;
  margin-left: 5px;
  margin-bottom: 5px;
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
.btn.active {
  color: #fff;
  background-color: #008080;
}
.btn.active:hover {
  color: #fff;
  background-color: #008080;
}

</style>
