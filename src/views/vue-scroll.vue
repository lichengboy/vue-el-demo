<!-- 导航定时滚动 -->
<template>
  <div id="demo">
    <ul class="list">
      <li
        v-for="(item, index) in ulList"
        :key="item.id"
        :class="!index && play ? 'toUp' : ''"
      >
        {{ item.msg }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  mounted() {
    setInterval(this.startPlay, 2000);
  },
  data() {
    return {
      ulList: [
        { msg: "这是第一条信息" },
        { msg: "这是第二条信息" },
        { msg: "这是第三条信息" },
      ],
      play: false,
    };
  },
  methods: {
    startPlay() {
      let that = this;
      that.play = true; //开始播放
      setTimeout(() => {
        that.ulList.push(that.ulList[0]); //将第一条数据塞到最后一个
        that.ulList.shift(); //删除第一条数据
        that.play = false; //暂停播放
      }, 500);
    },
  },
};
</script>

<style lang="scss" scoped>
.toUp {
  margin-top: -40px;
  transition: all 0.5s;
}

.list {
  list-style: none;
  width: 200px;
  text-align: center;
  overflow: hidden;
  height: 40px;
  padding: 0;
  margin: 0;
  border: 1px solid #ccc;
}
li {
  text-align: left;
  height: 40px;
  line-height: 40px;
}
</style>
