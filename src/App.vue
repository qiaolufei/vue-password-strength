<template>
  <div id="app">
   <input type="text"   v-if="visible" class="password" placeholder="请输入密码(最长16位)" @input="strength()" maxlength="16" v-model="password"/>
   <input type="password"   v-else class="password" placeholder="请输入密码(最长16位)" @input="strength()" maxlength="16" v-model="password"/>
   <img class="img" v-if="visible" src="./assets/ture.png" @click="changeVisible()">
   <img class="img" v-else src="./assets/false.png" @click="changeVisible()">
   <div class="strengthTip">
    <div v-show="strengthNum > 0" class="tip1"></div>
    <div v-show="strengthNum >1" class="tip2"></div>
    <div v-show="strengthNum > 2" class="tip3"></div>
    <div v-show="strengthNum > 3" class="tip4"></div>
    <span v-if="strengthNum == 0" class="tipText"></span>
    <span v-else-if="strengthNum == 1" style="color:#F24743" class="tipText">弱</span>
    <span v-else-if="strengthNum == 2" style="color:#F9AE35" class="tipText">中</span>
    <span v-else-if="strengthNum == 3" style="color:#2DAF7D" class="tipText">强</span>
    <span v-else style="color:#4C9EFF" class="tipText">很强</span>
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
      strengthNum: 0, //密码强度 0,1,2,3,4（弱、中、强、很强）
    }
  },
  methods: {
    changeVisible () {
      this.visible = !this.visible
    },
    strength () {
      let num = 0;
      if(this.password.length < 6){//最初级别
      num = 0;
      }
      if(/\d/.test(this.password)){//如果用户输入的密码 包含了数字
      num++;
      }
      if(/[a-z]/.test(this.password)){//如果用户输入的密码 包含了小写的a到z
      num++;
      }
      if(/[A-Z]/.test(this.password)){//如果用户输入的密码 包含了大写的A到Z
      num++;
      }
      if(/\W/.test(this.password)){//如果是非数字 字母 下划线
      num++;
      }
      this.strengthNum = num;
      console.log(this.strengthNum)
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
    border: 2px solid #2DAF7D;
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
  justify-content:center; //水平居中
  align-items:center; //垂直居中
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif
}
.tip1, .tip2, .tip3, .tip4{
  width: 55px;
  height: 10px;
  border-radius: 3px;
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
.tip4{
  background-color: #4C9EFF;
  margin-left: 5px;
}
.tipText{
  margin-left: 5px;
}
</style>
