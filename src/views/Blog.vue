<template>
  <div class="page">
    <el-card shadow="always" body-style="padding:0px">
      <!-- 开头开始 -->
      <div class="item">
        <div class="item-main-blog">
          <el-image :src="pic">
            <div slot="error" class="image-slot"></div>
          </el-image>
          <h1>{{ title }}</h1>
        </div>
        <div class="item-tags">
          <span class="tag-time"
            ><i class="el-icon-s-cooperation" style="margin-right:5px"></i
            >{{ date }}</span
          >
          <span class="tag-classify"
            ><i class="el-icon-s-promotion" style="margin-right:5px"></i
            >{{ classify }}</span
          >
        </div>
        <p>{{ gist }}</p>
      </div>
      <!-- 开头结束 -->
      <!-- 骨架开始 -->
      <!-- 骨架结束 -->
      <div class="detail" v-if="content">
        <mavon-editor
          v-model="content"
          default_open="preview"
          defaultOpen="preview"
          :toolbarsFlag="false"
          :subfield="false"
          :boxShadow="false"
          style="padding:0px!important"
        ></mavon-editor>
      </div>
      <div class="footer">
        <div @click="toGo(prev._id)" class="btn prev">
          <p>←上一篇</p>
          <p>{{ prev.title ? prev.title : "没有更多" }}</p>
        </div>
        <div @click="toGo(next._id)" class="btn next">
          <p>下一篇→</p>
          <p>{{ next.title ? next.title : "没有更多" }}</p>
        </div>
      </div>
    </el-card>

    <comment
      :comments="comments"
      :articleId="articleId"
      @update="update"
      @setTextarea="setTextarea"
    ></comment>
  </div>
</template>

<script>
import Comment from "../components/comment";

export default {
  data() {
    return {
      title: "",
      date: "",
      category: [],
      gist: "",
      content: "",
      comments: [],
      articleId: null,
      prev: {},
      next: {},
      pic: "",
      classify: "",
    };
  },
  created() {
    this.content = localStorage.getItem("content")
  },
  mounted: function() {
    // 移动
    console.log("5555555");
    var hd = document.getElementById("header");
    var headerwid = hd.offsetHeight;
    window.scrollTo(0, headerwid);
    this.init();
  },
  methods: {
    init: function() {
      if (this.$route.params.id) {
        this.articleId = this.$route.params.id;
        this.$http({
          method: "get",
          url: "articleDetail/" + this.$route.params.id,
        }).then((res) => {
          let {
            comments,
            title,
            date,
            /* content, */
            gist,
            category,
            prev,
            next,
            classify,
            pic,
          } = res.data;

          this.title = title;
          this.date = date;
          /* this.content = content; */
          this.gist = gist;
          this.category = category;
          this.prev = prev;
          this.next = next;
          this.classify = classify;
          this.pic = pic;
          document.getElementsByClassName("el-image")[0].style.opacity = 1
          if (comments) {
            for (let i = 0; i < comments.length; i++) {
              comments[i]["open"] = false;
              comments[i]["to_uid"] = comments[i]["from_uid"];
              comments[i]["to_uname"] = comments[i]["from_uname"];
            }
            this.comments = comments;
          }
        });
      }
    },
    update: function() {
      this.init();
    },
    /**
     * 改变输入框状态
     * index评论序号
     * open 该评论下输入框开否
     * to_uid 该评论下目标用户id
     * to_uname 该评论下目标name
     */
    setTextarea: function(params) {
      let { index, open, to_uid, to_uname } = params;
      let comments = this.comments;
      // console.log(params)
      if (to_uid) {
        comments[index]["to_uid"] = to_uid;
        comments[index]["to_uname"] = to_uname;
      }
      comments[index]["open"] = open;
      // debugger
      this.comments = comments;
    },
    toGo: function(id) {
      if (id) {
        this.$router.push({ path: `/detail/${id}` });
        // this.$router.push({ path: '/detail/'+id});

        // this.$router.push({ path: '/visiter'});
      }
    },
  },
  components: {
    Comment,
  },
  watch: {
    //监听路由参数变化后刷新页面
    $route() {
      this.init();
      /* Math.animation(
        document.documentElement.scrollTop,
        0,
        0,
        "Quart.easeOut",
        function(value) {
          document.documentElement.scrollTop = value;
          document.body.scrollTop = value;
        }
      ); */
    },
  },
};
</script>

<style lang="scss" scoped>
.wrapper {
  background: #f8f8fd;
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.4), 0 0 30px rgba(10, 10, 0, 0.1) inset;
  padding: 10px;
  & > .title {
    font-size: 16px;
    text-align: center;
    font-weight: 500;
  }
  & > .some {
    text-align: center;
    color: #999;
    margin: 10px 0;
    padding-bottom: 10px;
    .iconfont {
      color: #666;
      margin: 0 5px 0 0;
    }
    .date {
      margin: 0 10px 0 0;
      vertical-align: middle;
    }
    .category {
      vertical-align: middle;
      & > span {
        margin-right: 5px;
      }
    }
  }
}
.footer {
  display: flex;
  justify-content: space-between;
  margin: 20px 20%;
  border-radius: 6px;
  .btn {
    text-align: center;
    background: #fff;
    color: #666;
    padding: 10px;
    flex: 1;
    border: 1px solid #ddd;
    transition: all 0.3s;
    overflow: hidden;
    cursor: pointer;
    &:hover {
      background: #3b99fc;
      color: #fff;
    }
    p {
      width: 100%;
      overflow: hidden;
      text-overflow: ellipsis;
      white-space: nowrap;
    }
    &.prev {
      border-right: none;
    }
  }
}

@media (min-width: 768px) {
  //pc
  .wrapper {
    padding: 20px;
    & > .title {
      font-size: 28px;
    }
    & > .some {
      margin: 10px 0 40px;
      border-bottom: 1px solid #eee;
      padding-bottom: 20px;
      .iconfont {
        color: #666;
        margin: 0 5px 0 0;
      }
      .date {
        margin: 0 20px 0 0;
      }
    }
  }
}

.item {
  margin: 20px 25px 40px 25px;
}
.item .item-main-blog {
  width: 100%;
  position: relative;
  overflow: hidden;
  border-radius: 15px;
  min-height: 95px;
  background-color: #eee;
}
.item-main-blog h1 {
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
.item .item-tags {
  display: flex;
  justify-content: start;
  margin-top: 10px;
}
.item .item-tags span {
  width: 150px;
  height: 36px;
  border-radius: 20px;
  background-color: rgba(255, 185, 0, 0.1);
  color: #ffb900;
  margin-right: 20px;
  text-align: center;
  line-height: 36px;
  overflow: hidden;
}

.item .item-tags .tag-classify {
  background-color: rgba(255, 78, 106, 0.1);
  color: #ff4e6a;
}
.item p {
  text-align: start;
  margin: 15px 0;
}
.image-slot {
  position: relative;
  height: 480px;
  width: 882px;
  background-color: #ccc;
}

.el-image {
  width: 100%;
  height: 100%;
  opacity: 0;
  -webkit-transition: opacity 0.6s ease-in-out;
	-moz-transition: opacity 0.6s ease-in-out;
	-o-transition: opacity 0.6s ease-in-out;
	-ms-transition: opacity 0.6s ease-in-out;
	transition: opacity 0.6s ease-in-out;
}



</style>
