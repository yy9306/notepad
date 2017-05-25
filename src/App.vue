<template>
  <div id="app" :class="[getTheme]">
    <v-header @tools="changePages"></v-header>
    <section class="container">
       <n-add></n-add>
       <n-list></n-list>
       <n-sidebar :is-show="tools"
                  @opentable="table=true;tools=false"
                  @cleardialog="clearData"
                  @openTheme="theme=true;tools=false;"
       ></n-sidebar>
    </section>
    <n-theme :is-show="theme"></n-theme>
    <event-table :isShow="table" @deldialog="delData"></event-table>
    <n-dialog :msg="title" v-show="dialog" @cancel="dialog = false" @sure="sureDialog"></n-dialog>
  </div>
</template>

<script>
 import vHeader from './components/header'
 import nAdd from './components/event_add'
 import nList from './components/event_list'
 import nSidebar from './components/sidebar'
 import nTheme from './components/theme'
 import nDialog from './components/dialog'
 import eventTable from './components/event_table'
export default {
  components: {vHeader,nAdd,nList,nSidebar,nTheme,nDialog,eventTable},
  data() {
    return {
      tools: false,
      theme: false,
      table: false,
      title: '',
      dialog: false,
      dialog_type: '',
      del_info: {
          index: 0,
          id: 0
      }
    }
  },
  methods: {
    changePages() {
      if(this.table){
        this.table = false
      }else if(this.theme){
        this.theme = false
      }else{
        this.tools = !this.tools
      }
    },
    clearData() {
       this.tools = false;
       this.dialog = true;
       this.dialog_type = 'clear';
       this.title = '清空后无法恢复，你确认吗？'
    },
    delData(index,id){
        this.dialog = true;
        this.dialog_type = 'del';
        this.title = '删除后无法恢复，确认删除吗？';
        this.del_info = {
            index: index,
            id : id
        }
    },
    sureDialog() {
      switch(this.dialog_type){
        case 'clear':
            this.$store.dispatch('clearevent')
            break;
        case 'del':
            this.$store.dispatch('delevent',this.del_info);
            break;
      }
      this.dialog = false
    }
  },
  computed: {
    getTheme() {
      return this.$store.getters.getTheme;
    }
  }
}
</script>
<style lang="scss" rel="stylesheet/scss" src="../static/theme.scss"></style>
<style lang="scss">
html,body,ul,li,input{
    margin:0;
    padding:0;
}
body{
    font-size: 16px;
    font-family: "Helvetica Neue", Helvetica, "microsoft yahei", arial, STHeiTi, sans-serif;
}
input,button{
    -webkit-tap-highlight-color: transparent;
}
input[type=text]{
    -webkit-appearance: none;
}
button{
    padding:7px 0;
    outline: none;
    text-align: center;
    border-radius: 4px;
    box-sizing: border-box;
    font:{
        size:inherit;
        family: inherit;
    }
    cursor: pointer;
}
body,#app{
    width:100%;
    overflow-x: hidden;
}
ul{
    list-style: none;
}
.container{
    width:100%;
    padding: 0 10px;
    max-width:800px;
    margin:auto;
    box-sizing: border-box;
    &.hide{
        display: none;
    }
}
.dialog-enter-active, .dialog-leave-active {
    transition: opacity .3s;
}
.dialog-enter, .dialog-leave-to{
    opacity: 0;
}
</style>
