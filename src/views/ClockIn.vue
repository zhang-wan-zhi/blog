<template>
  <div class="clockindex">
    <div class="title">
      <h2>2021</h2>
      <div class="link-top">
        <div class="link-hight"></div>
      </div>
    </div>
    <div class="timeline">
      <el-timeline :reverse="reverse">
        <el-timeline-item
          v-for="(activity, index) in activities"
          :key="index"
          :timestamp="activity.date.slice(5,9)"
          color="#ff4e6a"
          placement="top"
        >
          {{ activity.title }}
        </el-timeline-item>
      </el-timeline>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      isClockIn: false,
      clockInDays: [],
      activities: [],
    };
  },
  methods: {
    ClockIn(e) {
      this.clockInDays.push(e);
      console.log("clockInDays", this.clockInDays);
    },
  },
  mounted() {
    this.$http({
      url: 'articleList',
      method: 'post',
    }).then((e) => {
      console.log('eee',e.data);
      this.activities = e.data
    })
  }
};
</script>
<style>
.clockindex {
  background-color: #fff;
  padding: 20px;
}
.is-selected {
  color: #1989fa;
}
.clockIn {
  width: 100%;
  height: 100%;
  background-color: red;
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

h2 {
  text-align: left;
  margin: 20px 0 5px 0;
}
.timeline {
  margin: 20px 10px;
}
.el-timeline-item__wrapper {
  display: flex;
}
.el-timeline-item__content {
  margin-left: 20px;
}
.el-timeline-item__tail {
  border-left: 2px solid rgba(255,78,106,.2);
}
</style>
