<template>
  <div id="app">
    <header>
      <div class="header-content clear">
        <a href="javascript:void(0);" class="logo">
          <img src="./assets/images/logo.png" alt="豆瓣" class="logo-icon"> 豆瓣
        </a>

      </div>
    </header>
    <div class="swiper-container">
      <div class="swiper-wrapper">
        <!-- <div class="swiper-slide home">
        </div> -->
        <div class="swiper-slide">
          <div class="bg loading" :style="'background-image: url(' + bgUrl + ');'"></div>
          <div class="barrage" id="barrage"></div>
          <div class="footer">
            <ul class="list">
              <li v-for="(item, index) in data" :key="index" @click="changeActive($event, index)" :class="{'active': activeIndex === index}">
                <div class="poster">
                  <img class="poster-img" :src="'../static/images/' + item.poster">
                </div>
                <p class="item-name">{{item.name}}</p>
              </li>
            </ul>
            <div class="new-barrage">
              <button class="barrage-ctrl" @click="toggleBarrage" :class="this.showbarrage ? 'open' : 'close'"></button>
              <form class="clear" method="post" @submit="newBarrage" action="javascript:;">
                  <button type="submit" class="barrage-submit">发送</button>
                  <input class="barrage-input" type="text" autocomplete="off" maxlength="30" placeholder="发条弹幕试试٩(๑❛ᴗ❛๑)۶">
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import "./assets/css/style.css";
import Swiper from "swiper";
import "./assets/swiper/swiper.css";
import data from "./assets/json/tv.json";
export default {
  name: "app",
  data() {
    return {
      data: data,
      rowWidthArr: new Array(10).fill(0).map((x, i) => i),
      active: data[0],
      activeIndex: 0,
      timer: null,
      showbarrage: true,
      $barrage: null,
      $bg: null,
      bgUrl: "../static/images/" + data[0].bg,
      colors: ["#fff", "pink", "#ff8c00", "#adff2f", "#6cc"]
    };
  },
  mounted() {
    this.$barrage = this.$el.querySelector("#barrage");
    this.$bg = this.$el.querySelector(".bg");
    this.initSwiper();
    this.barrage();
  },
  methods: {
    initSwiper() {
      let swiper = new Swiper(".swiper-container", {
        direction: "vertical",
        slidesPerView: 1,
        mousewheel: true,
        speed: 500
      });
    },
    changeBg() {
      let img = new Image();
      img.src = "../static/images/" + this.active.bg;
      img.onload = () => {
        let opacity = 0
        this.$bg.style.opacity = opacity;
        this.bgUrl = "../static/images/" + this.active.bg;
        let bgTimer = setInterval(() => {
          if(opacity >=1) {
            clearInterval(bgTimer);
          } else {
             opacity += 0.2;
            this.$bg.style.opacity = opacity;
          }
        }, 30);
      };
    },
    barrage() {
      let barrageList = this.active.barrage.split("&");
      let i = 0;
      this.rowWidthArr = this.rowWidthArr.sort(function(x, y){
        return Math.random() - 0.5;
      });
      this.timer = setInterval(() => {
        let min = Math.min(...this.rowWidthArr);
        let row = this.rowWidthArr.indexOf(min);
        if (min >= 1000) {
          this.rowWidthArr = this.rowWidthArr.map(v => {
            return v - 1000;
          });
        }
        this.initBarrageItem(barrageList[i], row);
        i++;
        if (i === barrageList.length) {
          i = 0;
        }
      }, 500);
    },
    initBarrageItem(data, index, bool) {
      let $barrage = this.$barrage;
      let rowHeight = 40;
      let item = document.createElement("p");
      let speed = 120 + (Math.random() - 0.5) * 20;
      let bodyWidth = document.body.clientWidth;
      item.innerText = data;
      if(bool) item.className = 'mine';
      $barrage.appendChild(item);

      let itemWidth = parseInt(item.getBoundingClientRect().width);
      let t = (itemWidth + bodyWidth) / speed ;
      this.rowWidthArr[index] = this.rowWidthArr[index] + itemWidth;
      item.style.color = this.colors[
        parseInt(this.colors.length * Math.random())
      ];
      item.style.top = index * rowHeight + "px";
      let w = itemWidth + bodyWidth;
      item.style.transition = "transform " + t + "s linear 0s";
      item.style.transform =
        "translateX(-" + w + "px) translateY(0) translateZ(0)";
      setTimeout(function() {
        item.remove();
      }, parseInt(t * 1050));
    },
    changeActive(e, index) {
      this.$bg.parentNode.style.backgroundImage =
        "url(../static/images/" + this.active.bg + ")";
      this.active = this.data[index];
      this.activeIndex = index;
      clearInterval(this.timer);
      this.changeBg();
      this.$barrage.innerHTML = "";
      if(this.showbarrage) this.barrage();
    },
    newBarrage(e) {
      let form = e.target;
      let input = e.target.querySelector('.barrage-input');
      let min = Math.min(...this.rowWidthArr);
      let row = this.rowWidthArr.indexOf(min);
      this.initBarrageItem(input.value, row, true);
      input.value = '';
      return false;
    },
    toggleBarrage() {
      this.showbarrage = !this.showbarrage;
      if(!this.showbarrage) {
        clearInterval(this.timer);
        this.$barrage.innerHTML = "";
      } else {
        this.barrage();
      }
    }
  }
};
</script>

<style lang="less">
html,
body {
  position: relative;
  height: 100%;
}

header {
  position: fixed;
  width: 100%;
  z-index: 100;
  height: 100px;
  background: url(./assets/images/head_top_mask.png) bottom repeat-x;
  .header-content {
    margin: 8px 20px;
    line-height: 28px;
  }
  .logo {
    float: left;
    color: #ffffff;
    font-size: 13px;
    font-weight: bold;
    img {
      float: left;
      margin-top: 5px;
      margin-right: 6px;
      width: 16px;
      height: 16px;
    }
  }
}

.swiper-container {
  position: absolute;
  width: 100%;
  height: 100%;
  margin-left: auto;
  margin-right: auto;
}
.swiper-slide {
  /* Center slide text vertically */
  // display: -webkit-box;
  // display: -ms-flexbox;
  // display: -webkit-flex;
  // display: flex;
  // -webkit-box-pack: center;
  // -ms-flex-pack: center;
  // -webkit-justify-content: center;
  // justify-content: center;
  // -webkit-box-align: center;
  // -ms-flex-align: center;
  // -webkit-align-items: center;
  // align-items: center;

  background: center no-repeat #fff;
  background-size: cover;
  .bg {
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    width: 100%;
    background: center no-repeat #fff;
    background-size: cover;
  }
}
.home {
  background-image: url(../static/images/bg_0.jpg);
}
.footer {
  position: absolute;
  width: 100%;
  bottom: 20px;
}
.list {
  white-space: nowrap;
  padding-left: 10px;
  position: relative;
  text-align: center;
  li {
    display: inline-block;
    list-style: none;
    margin: 0;
    cursor: pointer;
    width: 90px;
    .poster-img {
      box-shadow: 2px 2px 6px 1px rgba(0, 0, 0, 0.3);
    }
    .item-name {
      font-size: 12px;
      color: #fff;
      text-shadow: 0 0 2px rgba(0, 0, 0, 0.3);
    }
    &.active {
      .poster-img {
        width: 86px;
        height: 120px;
        border: 2px solid #fff;
      }
    }
  }
}

.poster-img {
  width: 72px;
  height: 100px;
  transition: all .3s linear;
}

.barrage {
  position: absolute;
  width: 100%;
  top: 50px;
  bottom: 50px;
  left: 0;

  p {
    position: absolute;
    left: 100%;
    padding: 0 14px;
    font-size: 13px;
    line-height: 2;
    color: #fff;
    white-space: nowrap;
    border-radius: 13px;
    background: rgba(0, 0, 0, 0.5);
    transform: translateX(0) translateY(0) translateZ(0);
    text-shadow: 0 0 rgba(0, 0, 0, 0.84);

    &.mine {
      border: 1px solid;
      color: #ffeb3b !important;
      padding-left: 34px;
      background-image: url(./assets/images/star.png);
      background-position: 8px center;
      background-repeat: no-repeat;
      background-size: 20px;
    }
  }
}
.new-barrage {
  position: relative;
  background: #fff;
  height: 30px;
  width: 600px;
  margin: 30px auto 0;
  border-radius: 17px;
  font-size: 12px;
  input, button  {
    font-size: 12px;
    color: #454545;
  }
}
.barrage-submit {
  float: right;
  width: 45px;
  margin-right: 10px;
  line-height: 30px;
  border: none;
  background: none;
}
.barrage-input {
  position: relative;
  display: block;
  top: 6px;
  margin: 0 60px;
  width: 480px;
  border-top: none;
  border-bottom: none;
  border-left: 1px solid #dbdbdb;
  border-right: 1px solid #dbdbdb;
  background: #fff;
  line-height: 18px;
  text-align: left;
  padding: 0 10px;
}
.barrage-ctrl {
  float: left;
  margin-left: 20px;
  width: 30px;
  height: 31px;
  background:  no-repeat center transparent;
  background-size: contain;
  border: none;
  &.open {
    background-image: url(./assets/images/barrage_open.png);
  }
  &.close {
    background-image: url('./assets/images/barrage_close.png');
  }
}
</style>
