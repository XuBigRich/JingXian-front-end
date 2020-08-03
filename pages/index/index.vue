<template>
	<view class="content">
		<view class="title">
			<p>登录</p>
		</view>
		<view>
			<p>账号</p>
			<input type="text" v-model="form.username" class="username">
			<p>密码</p>
			<input type="password" v-model="form.password" class="username">
		</view>
		<view>
			<button type="primary" class="login" @click="submit">登录</button>
		</view>
		<uni-popup ref="popup" type="message">
			<uni-popup-message type="success" :message="info" :duration="2000"></uni-popup-message>
		</uni-popup>
		<uni-popup ref="hint" type="dialog">
			<uni-popup-dialog type="input" :content="message" :duration="2000" :before-close="true" @close="close" @confirm="confirm"></uni-popup-dialog>
		</uni-popup>
	</view>
</template>

<script>
	import uniPopup from '@/components/uni-popup/uni-popup.vue'
	import uniPopupMessage from '@/components/uni-popup/uni-popup-message.vue'
	import uniPopupDialog from '@/components/uni-popup/uni-popup-dialog.vue'

	export default {
		components: {
			uniPopup,
			uniPopupMessage,
			uniPopupDialog
		},
		data() {
			return {
				info: '',
				message: '',
				form: {
					username: '',
					password: '',
				}
			}
		},
		methods: {
			submit() {
				if (this.form.username == '' || this.form.username == null) {
					this.info = "账号为空！";
					this.$refs.popup.open()
					return;
				}
				if (this.form.password == "" || this.form.password == null) {
					this.info = "密码为空！";
					this.$refs.popup.open()
					return;
				}
				console.log("发送请求");
				uni.request({
					url: "http://127.0.0.1:8080/login",
					header: {
						"Content-Type": "application/x-www-form-urlencoded"
					},
					data: {
						username: this.form.username,
						password: this.form.password,
					},
					success: (res) => {
						if (true) {
							console.log("登陆成功");
						} else {
							console.log("登陆失败")
						}
					},
				})
			},
			close(done) {
				// TODO 做一些其他的事情，before-close 为true的情况下，手动执行 done 才会关闭对话框
				// ...
				done()
			},
			/**
			 * 点击确认按钮触发
			 * @param {Object} done
			 * @param {Object} value
			 */
			confirm(done, value) {
				// 输入框的值
				console.log(value)
				// TODO 做一些其他的事情，手动执行 done 才会关闭对话框
				// ...
				done()
			},

		},
	}
</script>

<style scoped>
	.title {
		font-weight: bold;
		margin: 10rpx 0 40rpx 0;
		font-size: 44rpx;
		color: white;
	}

	.username {
		height: 80rpx;
		margin: 10rpx 0 40rpx 0;
		width: 600rpx;
		border-radius: 10rpx;
		border: #007aff 2rpx solid;
		background-color: rgba(200, 199, 204, 0.36);
	}

	.content {
		background-size: 100% 100%;
		padding: 70rpx;
		margin: 0 auto;
		text-align: center;
		height: 90.3vh;
	}

	.login {
		width: 100%;
		margin-top: 30rpx;
		color: white;
	}
</style>
