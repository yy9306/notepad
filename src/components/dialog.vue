<template>
 <div class="dialog">
    <div class="dialog-wrapper">
       <div class="dialog-header">
          <span class="dialog-header-title">提示</span>
       </div>
       <div class="dialog-content">
          {{msg}}
       </div>
       <div class="dialog-btns">
          <button type="button" class="cancel-btn" name="button" @click="cancelEvent">取消</button>
          <button type="button" class="sure-btn" name="button" @click="sureEvent">确定</button>
       </div>
    </div>
 </div>
</template>

<script>
 export default{
   props: {
     msg: {
       type: String,
       default: '提示'
     }
   },
   methods: {
     cancelEvent() {
       this.$emit('cancel')
     },
     sureEvent() {
       this.$emit('sure')
     }
   }
 }
</script>

<style lang="scss">
.dialog {
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    overflow: auto;
    background: rgba(0, 0, 0, .4);
    z-index:999;
    .dialog-wrapper {
        position: absolute;
        left: 50%;
        top: 20%;
        width:100%;
        max-width: 400px;
        transform: translateX(-50%);
        background: #fff;
        border-radius: 2px;
        box-shadow: 0 1px 3px rgba(0, 0, 0, .3);
        box-sizing: border-box;
        animation: dialog .5s;
    }
    .dialog-header {
        padding: 20px 20px 0;
    }
    .dialog-content {
        padding: 30px 20px;
        color: #475669;
        font-size: 18px;
        text-align: center;
    }
    .dialog-btns {
        padding: 10px 20px 15px;
        text-align: right;
        button {
            font-size: 14px;
        }
        .cancel-btn {
            width: 50px;
            background: #fff;
            border: 1px solid #c0ccda;
            color: #1f2d3d;
        }
        .sure-btn {
            width: 50px;
            margin-left: 5px;
            color: #fff;
            transition: background .3s ease-in;
        }
    }
}
@keyframes dialog {
    from{
        top: 15%;
    }
}
</style>
