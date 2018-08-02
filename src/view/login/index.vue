<template>
	<div class="my_l">
		<header class="top_bar">
		    <a onclick="window.history.go(-1)" class="icon_back"></a>
		    <h3 class="top_bar_name">京东登录</h3>
		</header>
		<main class="user_login_box">
		    <div class="login_dialog">　
		        <div class="_username">
		            <input type="text" ref="loginName" name="username" placeholder="请输入用户名" class="user_input" v-model="username"/>
		        </div>
		        <div class="_username u_passwd">
		            <input type="password" ref="loginPwd" @keyup.enter="goLogin" name="password" placeholder="请输入密码" class="user_input" v-model="password"/>
		        </div>
		        <div class="login_box">
		            <a @click="goLogin"  class="btn_login">登录</a>
		        </div>
				<div class="go_changePwd_box">
					<router-link tag="span" to="/changePwd">忘记密码</router-link>
				</div>
		        <div class="go_reg_box">
		            <router-link tag="span" to="/register">快速注册</router-link>
		        </div>
		    </div>
		</main>
	</div>
</template>
<script>
import { Message } from 'element-ui';
export default{
	data(){
		return {
			username:'',
			password:'',
			userInfo:{}
		}
	},
	methods:{
		async goLogin(){
			const _this = this;
			try {
				if(_this.username ==''){
					_this.prompt("请输入用户名",_this.$refs.loginName);
					return;
				}
				if(_this.password ==''){
					_this.prompt("请输入密码",_this.$refs.loginPwd);
					return;
				}
				let res = await _this.$http.post('/login',{
					loginName:_this.username,
					loginPawd:_this.password
				});
				if(res.status==200){
					_this.userInfo = res.data;
					if(_this.userInfo.status ==1){
						window.sessionStorage.userInfo = JSON.stringify(_this.userInfo);
						_this.loginSuccess();
						_this.$router.push('/');
					}else{
						_this.prompt(_this.userInfo.msg,_this.$refs.loginName);
					}
				}else {
					alert('请求错误');
				}
			} catch (error) {
				console.log(error)
			}
			
		},
		loginSuccess() {
			let _this = this;
			this.$message({
				showClose: true,
				message: '登陆成功！',
				type: 'success',
				duration:'2000',
				onClose(){
					_this.$router.push('/');
				}
			});
		},
		prompt(msg,field) {
			let _this = this;
			this.$alert(msg, 'err', {
				confirmButtonText: '确定',
				callback: action => {
					// this.$message({
					// type: 'info',
					// message: `action: ${ action }`
					// });
					field.focus();
					// field.parentNode.style.borderColor='red';
				}
			});
		}
	}
}
</script>
<style>
@import '../../assets/css/login.css';
</style>