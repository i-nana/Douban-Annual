<template>
  <div id="app" class="swiper-container">
  <div class="swiper-wrapper">
    <!-- <div class="swiper-slide home">
      <div class="content">
      </div>
    </div> -->
    <div class="swiper-slide" :style="'background-image: url(../static/images/' + data[0].bg + ');'">
      <div class="content">
        <div class="main">
          <div class="pull-left">
            
          </div>
        </div>
        <!-- <ul class="list">
          <li v-for="(item, index) in data" :key="index">
            <div class="poster">
              <img class="poster-img" :src="'../static/images/' + item.poster">
            </div>
          </li>
        </ul> -->
        <div class="barrage" id="barrage">

        </div>
      </div>

    </div>
  </div>
</div>
</template>

<script>
import "./assets/css/style.css"
import Swiper from  "swiper";
import "./assets/swiper/swiper.css";
import data from "./assets/json/tv.json"
export default {
  name: "app",
  data() {
    return {
      data: data,
      rowWidthArr: new Array(10).fill(0)
    }
  },
  mounted() {
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
    barrage() {
      let barrageList =  ["美人鱼无感。。", "我觉得星爷的美人鱼挺好的啊", "疯狂动物城 美人鱼 你的名字 湄公河行动 美国队长3 神奇动物在哪里", "为什么动物城不算评分最高的呢？", "卡顿了。。", "就魔兽没看了", "1246", "好棒！！！最喜欢的片子！！", "1 2 3 4 5 6 7 9 10", "美人鱼呵呵", "我去，居然有两部没看过", "除了《你的名字》都去影院看了诶", "那个爱宠的呢 这么萌居然没有", "动物一骑绝尘哈哈哈", "美人鱼真的不行", "疯狂动物城我居然在电影院看了三遍！！！！！！", "天启和魔兽分都太高了", "好想回到疯狂动物城那个时间如果一切可以重来", "年度最佳之一", "zootopia当之无愧", "看过8部", "动物城", "看到大鱼的分还不如美人鱼我就放心了", "讲个笑话：2016中国票房冠军：美人鱼", "看了三部，动物城，七月，魔兽", "3部动画片，1部喜剧，1部青春爱情片，5部动作片，其中2部超级英雄，1部游戏改编，看来还是大片受院线欢迎。4部国产，还不到一半。", "年初看了疯狂动物城 哈哈哈", "原来《疯狂动物城》不算在外语片评选范围内，喷了。", "我跟豆瓣三觀不合", "7部", "疯狂动物城最爱了", "这是咋评的？", "除了都看了", "除了你的名字都看了", "美人鱼很烂好吧", "只看了两部==", "大鱼海棠，美人鱼，呵呵呵", "大鱼海棠也能上", "永远善良勇敢，永远出乎意料", "魔兽居然只有第十 。", "最受关注是什么意思啊，是指看得人数排序么？", "继疯狂原始人之后最爱的动画，正能", "感谢单身，我看了全部……", "最受关注，应该是标记想看的人比较多", "大鱼海棠是个坑啊，唯一没去看的", "美人鱼美人鱼救命啊", "基本都看过2333333", "全部看过耶", "疯狂动物成", "感谢谈恋爱，我看了全部", "不是按分评的么低于7分两个是什么鬼。。。", "6部", "疯狂动物城实至名归", "名副其实", "那就是一个都市童话故事而已，一点都不现实...", "里面有两个特别不待见的低分片=，=", "大鱼垃圾了", "大鱼海棠是什么鬼？美人鱼是什么鬼？", "美人鱼和大鱼海棠……居然都在……", "美人鱼？？？？", "美人鱼是个什么鬼", "为什么没有算在最高评分外语电影里？", "豆瓣最棒！", "最受关注的只有第一个可以看。成功率真TM低！", "今年评分最高的难道不是这个？8.8比9.2高吗？", "9/10", "我居然全看过了", "9排10前面真的好吗", "疯狂动物城 美人鱼 湄公河 美队", "疯狂动物城剧情虽然是经典式的，看到后半段基本能猜出来，但是故事讲得很好", "美人鱼居然第二受关注，粉丝的钱有这么好挣吗", "有美人鱼没毛病, 说的是最受关注.", "只看过5部！最受关注不是很值得看。。", "居然只差神奇动物没有看 上映时候是最念叨的", "看了7部", "两部没看hh", "盗墓笔记", "看过五分三", "当之无愧", "我到现在也不懂 疯狂动物城好在哪里", "美人鱼？？？", "4部", "疯狂动物城妥妥的", "美人鱼", "有两部国产的没看", "全部看过  厉害了我", "你的名字没看过，不过动物城完美超过其他各个作品", "这大白条弹幕把重要的都遮住了。。", "我觉得美国队长才是好玩的电影啊", "美人鱼？？？", "美人鱼票房啊", "第一第二都是动画片", "吗", "大鱼海棠好失望", "看了7/10", "感谢豆瓣挺过这一关。豆瓣最棒！", "动物乌托邦一骑绝尘", "这个是按评论数量排的吗？", "美人鱼乱入是怎么回事！！？？", "好几部都还看"];
     var i = 0;
     let timer = setInterval(() => {
       let min = Math.min(...this.rowWidthArr);
       let row = this.rowWidthArr.indexOf(min);
       if(min >= 1000) {
         this.rowWidthArr = this.rowWidthArr.map((v) => { return v - 1000 });
       }
       this.initBarrageItem(barrageList[i], row);
       i++;
       if(i === barrageList.length) {
        //  clearInterval(timer);
        i = 0;
       }
     }, 500);
    },
    initBarrageItem(data, index) {
      let $barrage = this.$el.querySelector('#barrage');
      let rowHeight = 40;
      let item = document.createElement('p');
      let speed =160 + (Math.random() - 0.5) * 20;
      let bodyWidth = document.body.clientWidth;
      item.innerText = data;
      $barrage.appendChild(item);

      let itemWidth = parseInt(item.getBoundingClientRect().width);
      let t = parseInt(( itemWidth + bodyWidth ) / speed);
      this.rowWidthArr[index] = this.rowWidthArr[index] + itemWidth;
      item.style.left = '100%';
      item.style.top = index * rowHeight + 'px';
      item.style.transition = 'left ' + t+'s linear';
      item.style.left = item.getBoundingClientRect().width * -1 + 'px';
      setTimeout(function() {
        item.remove();
      }, t * 1000)

    },
  }
};
</script>

<style lang="less">
html,
body {
  position: relative;
  height: 100%;
}
.swiper-container {
  position: absolute;
  width: 100%;
  height: 100%;
  margin-left: auto;
  margin-right: auto;
}
.swiper-slide {
  font-size: 18px;
  background: center no-repeat #fff;
  background-size: cover;

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
}
.home {
  background-image: url(../static/images/bg_0.jpg);
}
.list {
  white-space: nowrap;
  li {
    display: inline-block;
    list-style: none;
    margin: 0 10px;
    box-shadow: 2px 2px 6px 1px rgba(0, 0, 0, .3);
  }
}
.poster-img {
  width: 86px;
  height: 120px;
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
    background: rgba(0, 0, 0, .5);
    // transition: left 100ms linear;
  }
}
</style>
