<template>
  <div class="layui-fluid layui-form layui-form-pane" id="loginForm">
          <div class="layui-form-item">
            <label class="layui-form-label">用户名</label>
            <div class="layui-input-inline">
              <input name="username"  v-model="account.userName" lay-verify="required" placeholder="请输入用户名" autocomplete="off" class="layui-input" type="text">
            </div>
          </div>
          <div class="layui-form-item">
            <label class="layui-form-label">密码</label>
            <div class="layui-input-inline">
              <input name="password" v-model="account.userPassword" placeholder="请输入密码" autocomplete="off" class="layui-input" type="password">
            </div>
          </div>
          <div class="layui-form-item">
            <button class="layui-btn" lay-submit="" lay-filter="demo1" v-on:click="handleLogin">登陆</button>
            <button type="reset" class="layui-btn layui-btn-primary">取消</button>
          </div>
    </div>
</template>

<script src="static/layui/layui.js">
</script>
<script>
layui.use("layer", function() {
  layer = layui.layer;
});
export default {
  name: "login",
  data() {
    return {
      loading: false,
      account: {
        userName: "",
        userPassword: ""
      }
    };
  },
  methods: {
    handleLogin: function() {
      // layer.alert("登陆", {
      //     title: '成功'
      //   })
      //this.$router.push({path: '/home'});
      this.$http.post(
          "http://127.0.0.1:8888/user/login",this.account,{emulateJSON:true}
        )
        .then(
          response => {
            if(response.body.status==200){
              this.$router.push({path: '/home'});
            }else if(response.body.status==300){
layer.alert("用户名或密码不正确", {
          title: '错误'
})
            }
          }
        );
    }
  }
};
</script>
<style>
#loginForm {
  width: 600px;
  height: 400px;
  position: absolute;
  left: 50%;
  top: 50%;
  margin-left: -250px;
  margin-top: -100px;
}
</style>
