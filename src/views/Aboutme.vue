<template>
  <div class="aboutme">
    <el-card shadow="always" body-style="padding:20px">
      <div class="aboutme-head">
        <el-image
          :src="src"
          lazy
          style="width:880px;wight:500px;border-radius: 20px;"
        ></el-image>
        <h1>关于作者</h1>
      </div>
      <aplayer
        :autoplay="false"
        :music="{
          title: 'Mystery of Love',
          author: 'The Psychedelic Furs',
          url:
            'http://www.ihaoge.net/kw/antiserver.kuwo.cn/anti.s?rid=MUSIC_40169614&response=res&format=mp3|aac&type=convert_url&br=128kmp3&agent=iPhone&callback=getlink&jpcallback=getlink.mp3',
          pic:
            'https://gss3.bdstatic.com/84oSdTum2Q5BphGlnYG/timg?wapp&quality=80&size=b150_150&subsize=20480&cut_x=0&cut_w=0&cut_y=0&cut_h=0&sec=1369815402&srctrace&di=e7c1d819280a80b3d060fce64088b938&wh_rate=null&src=http%3A%2F%2Fimgsrc.baidu.com%2Fforum%2Fpic%2Fitem%2F32fa828ba61ea8d3680853379c0a304e251f58de.jpg',
          lrc: '[00:00.00]lrc here\n[00:01.00]aplayer',
        }"
      >
      </aplayer>
      <div class="title">
        <h2>博客相关</h2>
        <div class="link-top">
          <div class="link-hight"></div>
        </div>
      </div>
      <article>
        <p>创建时间：2021年1月18号-2021年1月22号</p>
        <p>技术栈：Vue + Express + Mongodb</p>
        <p>
          这个个人博客只是为了自己的兴趣爱好而建立的，所以可能会有许许多多的小BUG
        </p>
        <div class="link">
          <p>博客源码:</p>
          <a href="https://github.com/zhang-wan-zhi/vue-pic" target="_blank"
            >https://github.com/zhang-wan-zhi/vue-pic</a
          >
        </div>
      </article>
      <div class="title">
        <h2>作品相关</h2>
        <div class="link-top">
          <div class="link-hight"></div>
        </div>
      </div>
      <div class="title">
        <h2>关于我</h2>
        <div class="link-top">
          <div class="link-hight"></div>
        </div>
      </div>
      <article>
        <p>我是理科生，喜欢机械和爆炸，流星和烟花。</p>
        <p>喜欢摄影，不喜欢构图</p>
        <p>喜欢看电影，因为喜欢看电影</p>
        <p>喜欢动物，不喜欢虫子，除了蝴蝶和萤火虫</p>
        <p>然后和 我 干杯 遇到 失落沙洲</p>
      </article>
      <div class="title">
        <h2>关于摄影</h2>
        <div class="link-top">
          <div class="link-hight"></div>
        </div>
      </div>
      <div class="images">
        <el-image
          style="width: 400px; height: 400px"
          :src="images1"
          :preview-src-list="srcList1"
        >
        </el-image>
      </div>
    </el-card>
  </div>
</template>

<script>
import Aplayer from "vue-aplayer";
export default {
  data() {
    return {
      src: require("../../public/static/image/aboutme.png"),
      images1: require("../../public/static/image/1.jpg"),
      srcList1: [
        require("../../public/static/image/1.1.png"),
        require("../../public/static/image/1.2.png"),
      ],
    };
  },
  components: {
    Aplayer,
  },
  mounted() {
    var hd = document.getElementById("header");
    var headerwid = hd.offsetHeight;
    window.scrollTo(0, headerwid);
  },
};
</script>

<style>
.aboutme .aboutme-head {
  position: relative;
  margin-bottom: 20px;
}

.aboutme h1 {
  color: #fff;
  font-size: 2.5em;
  font-weight: 400;
  margin: 0;
  margin-top: 10px;
  padding-left: 1px;
  position: absolute;
  bottom: 0;
  width: 100%;
  box-sizing: border-box;
  text-transform: none;
  z-index: 1;
  padding: 25px;
  text-align: left;
}
.aboutme .aplayer {
  border-radius: 5px;
}
.aboutme h2 {
  text-align: left;
  margin: 20px 0 5px 0;
}
.link-top {
  position: relative;
  width: 100%;
  height: 1px;
  border-top: solid#eee 1px;
}
.link-hight {
  position: absolute;
  background-color: #ff4e6a;
  height: 5px;
  width: 2em;
  box-shadow: 0 2px 12px rgba(255, 78, 106, 0.85);
  bottom: -3px;
  border-radius: 10px;
  transition: width 0.75s;
}
.title:hover .link-hight {
  width: 4em;
}
.aboutme article {
  text-align: left;
  margin-top: 20px;
}
.aboutme article p {
  margin-top: 20px;
}
.aboutme article a {
  display: inline;
}
.aboutme article .link {
  display: flex;
  justify-content: start;
}
.aboutme article a {
  line-height: 60px;
  text-align: center;
  margin-left: 10px;
  color: #ff4e6a;
}
.aboutme .images {
  display: flex;
  margin-top: 20px;
}
</style>
