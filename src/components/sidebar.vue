<template>
  <div class="event-tools" :class="{'show-event-tools':isShow}">
    <ul class="tools-sidebar">
        <li>
          <button type="button" name="button" class="tools-btn" @click="openTheme">切换主题</button>
        </li>
        <li>
          <button type="button" name="button" class="tools-btn">下载数据</button>
        </li>
        <li>
          <button type="button" name="button" class="tools-btn" @click="openTable">编辑数据</button>
        </li>
        <li>
          <button type="button" name="button" class="tools-btn" @click="showDialog">清空数据</button>
        </li>
    </ul>
  </div>
</template>

<script>
 export default{
   props: {
    isShow:{
      type: Boolean,
      default: false
    }
  },
  methods: {
    openTheme() {
      this.$emit('openTheme');
    },
    showDialog() {
      this.$emit('cleardialog');
    },
    openTable(){
        this.$emit('opentable');
    },
  }
 }
</script>

<style scoped lang="scss">
.event-tools{
    position: fixed;
    top:0;
    left:0;
    bottom:0;
    width:250px;
    padding:100px 20px 30px;
    box-sizing: border-box;
    transform: translateX(-250px);
    transition: transform .3s;
    text-align: center;
    background: rgba(0,0,0,.5);
    font-size: 16px;
    z-index:9;
    &.show-event-tools{
        transform: translateX(0);
    }
    .tools-sidebar{
        & > li{
            line-height: 60px;
        }
    }
    .tools-btn{
        border: none;
        width:100px;
        height:40px;
        line-height: 26px;
        color: #fff;
        transition: background .3s ease-in;
    }
    pre{
        white-space: pre-wrap;
        font:{
            size: 14px;
            family:  arial,"microsoft yahei";
        }
        line-height: 20px;
    }
}
</style>
