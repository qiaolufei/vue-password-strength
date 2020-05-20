<template>
  <div id="app">
   <input type="text"   v-if="visible" class="password" placeholder="请输入密码(最长16位)" @input="strength()" maxlength="16" v-model="password"/>
   <input type="password"   v-else class="password" placeholder="请输入密码(最长16位)" @input="strength()" maxlength="16" v-model="password"/>
   <img class="img" v-if="visible" src="./assets/ture.png" @click="changeVisible()">
   <img class="img" v-else src="./assets/false.png" @click="changeVisible()">
   <div class="strengthTip">
    <span v-if="strengthNum != 0">密码强度：</span>
    <div v-show="strengthNum > 0" class="tip1"></div>
    <div v-show="strengthNum >1" class="tip2"></div>
    <div v-show="strengthNum > 2" class="tip3"></div>
   </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      password: '',
      visible:false,
      strengthNum: 0, //密码强度 1,2,3（弱、中、强）
    }
  },
  methods: {
    // 改变是否显示密码状态
    changeVisible () {
      this.visible = !this.visible
    },
    // 强度判断
    strength () {
      let num = 0;
      if(this.password.length < 6){//最初级别
        num = 0;
      } else {
        if(/\d/.test(this.password)){//如果用户输入的密码 包含了数字
        num++;
        }
        if(/[a-z]/.test(this.password) || /[A-Z]/.test(this.password)){//如果用户输入的密码 包含了小写的a到z
        num++;
        }
        if(/\W/.test(this.password)){//如果是非数字 字母 下划线
        num++;
        }
      }
      this.strengthNum = num;
    }
  }
}
</script>

<style lang="scss">
.password{
    width: 250px;
    height: 16px;
    padding: 12px 16px;
    font-size: 16px;
    position: fixed;
    margin: 0;
    vertical-align: top;
    outline: 0;
    box-shadow: none;
    border-radius: 10px 10px 10px 10px;
    border: 2px solid #c4c7ce;
    background: #fff;
    color: #222;
    overflow: hidden;
    ime-mode: active;
}
.img{
  height: 20px;
  position: fixed;
  top:20px;
  left: 250px;
}
.strengthTip{
  position: fixed;
  top: 60px;
  height: 20px;
  display: flex;
  flex-direction: row;
  justify-content:center;
  align-items:center;
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif
}
.tip1, .tip2, .tip3{
  width: 60px;
  height: 10px;
  border-radius: 3px;
  box-shadow: 3px 3px 1px #c4c7ce;
}
.tip1{
  background-color: #F24743;
}
.tip2{
  background-color: #F9AE35;
  margin-left: 5px;
}
.tip3{
  background-color: #2DAF7D;
  margin-left: 5px;
}
</style>
