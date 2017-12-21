<template>
<div id="app">
  <header>
    <div class="header-content clear">
      <a href="javascript:void(0);" class="logo">
        <img src="./assets/images/logo.png" alt="豆瓣" class="logo-icon">
        豆瓣
      </a>
    </div>
  </header>
  <div class="swiper-container">
    <div class="swiper-wrapper">
      <!-- <div class="swiper-slide home">
        <div class="content">
        </div>
      </div> -->
      <div class="swiper-slide" :style="'background-image: url(../static/images/' + active.bg + ');'">
        <div class="barrage" id="barrage"></div>
        <ul class="list">
          <li v-for="(item, index) in data" :key="index" @click="changeActive($event, index)">
            <div class="poster">
              <img class="poster-img" :src="'../static/images/' + item.poster">
            </div>
          </li>
        </ul>
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
      rowWidthArr: new Array(10).fill(0),
      active: data[0],
      colors: ['#fff', '#fff', '#009688', '#f44336', '#fff', '#2196f3']
    };
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
      let barrageList =
        "美人鱼大烂片&哈哈哈哈哈笑死我了&十部全中 盆盆盆&动物一骑绝尘哈哈哈&美人鱼6.9为啥在第二&疯狂动物城剧情虽然是经典式的，看到后半段基本能猜出来，但是故事讲得很好&这十部看了七部&1、2、3、4、5、8、9&最受关注的只有第一个可以看。成功率真TM低！&美人鱼？？？？&天启和魔兽分都太高了&最受关注不等于最好，这是按评论人数排的别搞错了&美人鱼票房啊&看了三部，动物城，七月，魔兽&这个是按评论数量排的吗？&吗&除了你的名字都看了&最受关注是什么意思啊，是指看得人数排序么？&6/10&美人鱼我是不服的&美人鱼跟大鱼海棠或成最大赢家&动物城吹在此&好喜欢&给钱了是吧&nimabi美人鱼 6.9排第二？？？？？？？？？？？？？？？？？？？、&美人鱼？？？&TEST&全部都看过~&看了7部&这个除了你的名字都看看过了&3部动画片，1部喜剧，1部青春爱情片，5部动作片，其中2部超级英雄，1部游戏改编，看来还是大片受院线欢迎。4部国产，还不到一半。&看了1 2 3 4  10&只有你的名字还没看了。。2016最后一天我要看掉你！！！&有意思我只没看过最后一部&疯狂动物城评分这么高&疯狂动物城刷了两遍&为什么没有算在最高评分外语电影里？&都看过。。。。。。&看了123579六部~&你个狡猾的狐狸&大鱼海棠是个坑啊，唯一没去看的&美人鱼真的不行&感谢豆瓣挺过这一关。豆瓣最棒！&美人鱼？excuse  me???&这大白条弹幕把重要的都遮住了。。&这是咋评的？&神奇动物在哪里的分怕是略高了点&1246&美人鱼？？？&公允&动画片另外归类吧，上面的最佳华语最佳外语都是指剧情片&讲个笑话：2016中国票房冠军：美人鱼&除了《你的名字》都去影院看了诶&我跟豆瓣三觀不合&求这张图片&除了湄公河和大鱼海棠没有看。&今年评分最高的难道不是这个？8.8比9.2高吗？&疯狂动物城实至名归&为什么动物城不算评分最高的呢？&大鱼海棠，美人鱼，呵呵呵&有两部国产的没看&美人鱼的确蛮不错的！&zootopia当之无愧&好想回到疯狂动物城那个时间如果一切可以重来&你的名字。大赞！！！！！&大鱼海棠也能上&当之无愧&我去，居然有两部没看过&疯狂动物城2刷&美人鱼无感。。&看了6部&里面有两个特别不待见的低分片=，=&4部&卡顿了。。&大鱼海棠不配&9排10前面真的好吗&美人鱼是个什么鬼&看了7/10&看过8部&原来《疯狂动物城》不算在外语片评选范围内，喷了。&7部&这样也要喷？键盘侠？？？动物城外语片这个&《疯狂动物城》，我居然看了，还不错，喜欢树懒&美人鱼的评分什么情况？&有美人鱼没毛病, 说的是最受关注.&天啊，这也是一片灾难啊，那么多实在是不怎么样的电影啊&美人鱼很烂好吧&盗墓笔记&美人鱼年度烂片没得跑&我爱的尼克来了&1 2 5 7 9 10&感谢谈恋爱，我看了全部&看了6部&寒战2 去哪里了&大家 晚上好&动物城实至名归&你的名字 疯狂动物城 美国队长 美人鱼&看到大鱼的分还不如美人鱼我就放心了&我广大wower竟然才够第十？&你的名字&5498488888888888888888888888888888888888888888888888&顶一发罗曼蒂克消亡史&驴得水哪里好看了？连电影都不是&只看过5，呵呵呵呵呵&10部看了6&还是柜子来了经典&湄公河行动绝*应该第一啊&哈&保卫豆瓣&我也觉得百鸟不该在上面&完蛋&11111&还有后来的&这评分最高榜单就像畅销书一样，是大家都喜欢看的。很好&也只有这几部能拿的出手了&1、2、4、8&湄公河让人失望 被高估的影片&湄公河怎么那么高&前三比较同意  后面的没怎么看过&看过6部，其中5部在电影院。&不是驴得水要黑马 而是国内哗众取宠的电影太多&啊&看了六部，算及格了&最爱路边野餐&往下走吧&1、2、4真的是虚高&....&人性&驴得水被高估，除了烂片太多，显然也是因为它并不高明的黑化式批判&湄公河行动还是不错的，但换成外国人的话，分数只能降低&踏雪寻梅给高&3&百鸟朝凤第4，情怀真是值钱啊。&驴得水排第一。。。。&追凶者也明明比较屌！！&最后悔的就是没去看驴得水啊~~~~~&国产片榜单漏了喊山&七月与安生？？？？？&驴得水？&歌曲好听啊&看了五部&再往后的zly&驴得水，要不是 有人一起，我都要中途李长乐&呵呵&无论被批与否 真性情才是豆瓣  如果因为被批就认怂  那就不是豆瓣了&今年真的没啥好片啊&《驴得水》连电影都不是，一部戏剧录像竟然是第一名。悲哉&驴得水电影感真的太少了，第一真不配！&真美好 好喜欢驴得水&怎么在七月与安生后面呢&百鸟朝凤这种水平也配&我觉得驴得水配不上这个&罗曼蒂克应该在第一位，真可惜档期没调好。&树大招风不是第一不服啊&我是来舔任素汐的～&厉害了&驴得水实至名归&就着city of&特地回来听BGM&我去正好iTunes在放city of stars&和我预想的不太一样啊&这两天都给他看完&你&都看过&艾玛BGM一上来就是lalaland&驴得水 湄公河&这都是些啥呀~~~~果然不靠谱&7K的投票也能作为参考么&驴得水 是一部悲剧&哇哦 city of stars~&这种电影居然评分最高  证明实在没有电影了&只看两部&1 2 4 都虚高了吧。。。8分啊。。&驴得水太让人眼瞎了，名不符实啊&这些能够进十佳的顶多也就是3部，其他也配？！&非常满意 今晚放假了 开始补&一个人占领弹幕真爽&七月与安生或许可以更高&只有5没看过了&驴得水实至名归&驴得水真心牛&七月与安生&也做了计划 按照它去执行&但是这首歌&谁能告诉我怎么切换到第二部&还有弹幕？？&欣赏BGM&看了7部&湄公河排第二我也真是没看懂&支持&哇塞，我看了两部&我认为前三分别是：路边野餐、我不是潘金莲、驴得水&前十看了三部，也是今年看的仅有的国产片。&树大招风不至于吧&坚定地乐观地、&给豆瓣比心&看了前两个&看了5部&看过一半 基本都是去电影院看的&就前看过一部，湄公河的评价似乎太高了点！";
      barrageList = barrageList.split("&");
      var i = 0;
      let timer = setInterval(() => {
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
          //  clearInterval(timer);
          i = 0;
        }
      }, 500);
    },
    initBarrageItem(data, index) {
      let $barrage = this.$el.querySelector("#barrage");
      let rowHeight = 40;
      let item = document.createElement("p");
      let speed = 100 + (Math.random() - 0.5) * 20;
      let bodyWidth = document.body.clientWidth;
      item.innerText = data;
      $barrage.appendChild(item);

      let itemWidth = parseInt(item.getBoundingClientRect().width);
      let t = (itemWidth + bodyWidth) / speed;
      this.rowWidthArr[index] = this.rowWidthArr[index] + itemWidth;
      item.style.left = "100%";
      item.style.color = this.colors[parseInt(this.colors.length * Math.random())];
      item.style.top = index * rowHeight + "px";
      item.style.transition = "left " + t + "s linear";
      item.style.left = item.getBoundingClientRect().width * -1 + "px";
      setTimeout(function() {
        // item.remove();
      }, parseInt(t * 1000));
    },
    changeActive(e, index) {
      this.active = this.data[index];
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
  padding-left: 10px;
  position: absolute;
  width: 100%;
  bottom: 100px;
  text-align: center;
  li {
    display: inline-block;
    list-style: none;
    margin: 0 0 0 10px;
    box-shadow: 2px 2px 6px 1px rgba(0, 0, 0, 0.3);
    cursor: pointer;
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
    background: rgba(0, 0, 0, 0.5);
    // transition: left 100ms linear;
  }
}
</style>
