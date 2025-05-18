<template>
	<view class="content">
		<view class="box" :style='{"minHeight":"100vh","width":"100%","padding":"360rpx 0 24rpx","background":"url(http://codegen.caihongy.cn/20241123/711cc904af7e41b6958532cf815eb5f2.jpg) no-repeat center top / 100% auto,#fff","height":"auto"}'>
			<view :style='{"border":"2rpx solid #fff","padding":"120rpx 48rpx 144rpx","margin":"100rpx 0 0","textAlign":"center","display":"flex","justifyContent":"space-between","alignContent":"flex-start","borderRadius":"60rpx","flexWrap":"wrap","background":"rgba(255,255,255,1)","width":"100%","position":"relative","height":"auto"}'>
				<image :style='{"margin":"0 auto 24rpx auto","borderRadius":"20rpx","top":"-80rpx","left":"40%","display":"block","width":"160rpx","position":"absolute","height":"160rpx"}' src="http://codegen.caihongy.cn/20241123/da8e5c4b661a4d9eaec7cf35075ba434.png" mode="aspectFill"></image>
				<view v-if="loginType==1" :style='{"border":"0px solid #1ccb96","margin":"0 0 48rpx 0","borderRadius":"20rpx","flexWrap":"wrap","background":"none","display":"flex","width":"calc(100% - 0px)","height":"auto"}' class="uni-form-item uni-column">
					<view :style='{"padding":"0 20rpx","color":"#fff","borderRadius":"8rpx 8rpx 0 0","textAlign":"left","background":"#B0CB5E","width":"auto","lineHeight":"60rpx","fontSize":"28rpx","minWidth":"160rpx"}' class="label">账号：</view>
					<input v-model="username" :style='{"border":"2rpx solid #9D9D9D","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"0 8rpx 8rpx 8rpx","textAlign":"left","background":"#fff","width":"100%","fontSize":"28rpx","lineHeight":"88rpx","height":"88rpx"}' type="text" class="uni-input" name="" placeholder="请输入账号" />
				</view>
				<view v-if="loginType==1" :style='{"border":"0px solid #1ccb96","margin":"0 0 48rpx 0","borderRadius":"20rpx","flexWrap":"wrap","background":"none","display":"flex","width":"calc(100% - 0px)","height":"auto"}' class="uni-form-item uni-column">
					<view :style='{"padding":"0 20rpx","color":"#fff","borderRadius":"8rpx 8rpx 0 0","textAlign":"left","background":"#B0CB5E","width":"auto","lineHeight":"60rpx","fontSize":"28rpx","minWidth":"160rpx"}' class="label">密码：</view>
					<input v-model="password" :style='{"border":"2rpx solid #9D9D9D","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"0 8rpx 8rpx 8rpx","textAlign":"left","background":"#fff","width":"100%","fontSize":"28rpx","lineHeight":"88rpx","height":"88rpx"}' type="password" class="uni-input" name="" placeholder="请输入密码" />
				</view>
				<view v-if="roleNum>1" :style='{"border":"0px solid #1ccb96","margin":"0 0 24rpx 0","borderRadius":"20rpx","flexWrap":"wrap","background":"none","display":"flex","width":"calc(100% - 0px)","height":"auto"}'>
					<view :style='{"padding":"0 20rpx","color":"#fff","borderRadius":"8rpx 8rpx 0 0","textAlign":"left","background":"#B0CB5E","width":"auto","lineHeight":"60rpx","fontSize":"28rpx","minWidth":"160rpx"}' class="label">用户类型：</view>
					<picker @change="optionsChange" :value="index" :range="options" :style='{"border":"2rpx solid #9D9D9D","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"0 8rpx 8rpx 8rpx","textAlign":"left","background":"#fff","width":"100%","fontSize":"28rpx","lineHeight":"88rpx","height":"88rpx"}'>
						<view class="uni-picker-type">{{options[index]}}</view>
					</picker>
				</view>
				

				
				<button v-if="loginType==1" class="btn-submit" @tap="onLoginTap" type="primary" :style='{"border":"0","padding":"0 40rpx","margin":"20rpx 20rpx 20rpx 0","color":"rgb(255, 255, 255)","display":"inline-flex","minWidth":"100%","justifyContent":"center","borderRadius":"8rpx","background":"linear-gradient(30deg, rgba(238,230,164,1) 0%, rgba(181,205,99,1) 100%)","width":"auto","lineHeight":"84rpx","fontSize":"32rpx","fontWeight":"600","height":"84rpx"}'>登录</button>
				<!-- #ifdef MP-WEIXIN -->
				<button v-if="loginType==1" class="btn-submit" open-type="getUserInfo" @getuserinfo="getUserInfo" type="primary" :style='{"border":"0","padding":"0 40rpx","margin":"20rpx 20rpx 20rpx 0","color":"rgb(255, 255, 255)","borderRadius":"8rpx","background":"linear-gradient(30deg, rgba(238,230,164,1) 0%, rgba(181,205,99,1) 100%)","width":"45%","lineHeight":"84rpx","fontSize":"32rpx","height":"84rpx","order":"20"}'>微信登录</button>
				<!-- #endif -->
				<button v-if="loginType==2" class="btn-submit" @tap="onFaceLoginTap" type="primary" :style='{"border":"0","padding":"0 40rpx","margin":"20rpx 20rpx 20rpx 0","color":"rgb(255, 255, 255)","display":"inline-flex","minWidth":"100%","justifyContent":"center","borderRadius":"8rpx","background":"linear-gradient(30deg, rgba(238,230,164,1) 0%, rgba(181,205,99,1) 100%)","width":"auto","lineHeight":"84rpx","fontSize":"32rpx","fontWeight":"600","height":"84rpx"}'>人脸识别登录</button>
				<view class="links" :style='{"width":"auto","padding":"0","margin":"20rpx 0 0","flexWrap":"wrap","display":"inline-flex","height":"auto"}'>
					<view class="link-highlight" @tap="onRegisterTap('yonghu')" :style='{"border":"0px solid #1ccb96","padding":"0 40rpx","margin":"0 20rpx 20rpx 0","color":"#fff","borderRadius":"8rpx","background":"linear-gradient(30deg, rgba(238,230,164,1) 0%, rgba(181,205,99,1) 100%)","display":"inline-flex","width":"auto","fontSize":"32rpx","lineHeight":"84rpx","height":"84rpx"}'>注册用户</view>
					<view class="link-highlight" @tap="onRegisterTap('congyezhe')" :style='{"border":"0px solid #1ccb96","padding":"0 40rpx","margin":"0 20rpx 20rpx 0","color":"#fff","borderRadius":"8rpx","background":"linear-gradient(30deg, rgba(238,230,164,1) 0%, rgba(181,205,99,1) 100%)","display":"inline-flex","width":"auto","fontSize":"32rpx","lineHeight":"84rpx","height":"84rpx"}'>注册从业者</view>
				</view>
				
				<view class="idea1" :style='{"width":"100%","background":"red","display":"none","height":"80rpx"}'>idea1</view>
				<view class="idea2" :style='{"width":"100%","background":"red","display":"none","height":"80rpx"}'>idea2</view>
				<view class="idea3" :style='{"width":"100%","background":"red","display":"none","height":"80rpx"}'>idea3</view>
			</view>
		</view>
	</view>
</template>

<script>
	import menu from '@/utils/menu'
	export default {
		data() {
			return {
				username: '',
				password: '',
                loginType:1,
				codes: [{
				  num: 1,
				  color: '#000',
				  rotate: '10deg',
				  size: '16px'
				}, {
				  num: 2,
				  color: '#000',
				  rotate: '10deg',
				  size: '16px'
				}, {
				  num: 3,
				  color: '#000',
				  rotate: '10deg',
				  size: '16px'
				}, {
				  num: 4,
				  color: '#000',
				  rotate: '10deg',
				  size: '16px'
				}],
				options: [
					'请选择登录用户类型',
				],
                optionsValues: [
					'',
                    'yonghu',
                    'congyezhe',
				],
				index: 0,
				roleNum:0,

				// #ifdef MP-WEIXIN
				code: '',
				// #endif
			}
		},
		onLoad() {
			let options = ['请选择登录用户类型'];
			let menus = menu.list();
			this.menuList = menus;
			for(let i=0;i<this.menuList.length;i++){
				if(this.menuList[i].hasFrontLogin=='是'){
					options.push(this.menuList[i].roleName);
					this.roleNum++;
				}
			}
			if(this.roleNum==1) {
				this.index = 1;
			}	
			this.options = options;
			this.styleChange()
		},
		onShow() {
			// #ifdef MP-WEIXIN
			let that = this
			uni.login({
				provider: 'weixin',
				success(res) {
					that.code = res.code
				}
			})
			// #endif
		},
		mounted() {
		},
		methods: {
			// #ifdef MP-WEIXIN
			async getUserInfo(e) {
				let that = this
				if (!this.optionsValues[this.index]) {
					this.$utils.msg('请选择登录用户类型')
					return
				}
				if (e.detail.errMsg === "getUserInfo:ok") {
					uni.showModal({
						content:'是否使用微信授权登录？',
						success:async (rs)=> {
							if(rs.confirm){
								let params = {
									code: that.code,
									encryptedData: e.detail.encryptedData,
									iv: e.detail.iv,
									rawData: e.detail.rawData,
									signature: e.detail.signature
								}
								let res = await that.$api.wxlogin(that.optionsValues[that.index], params)
								uni.removeStorageSync("useridTag");
								uni.setStorageSync("appToken", res.token);
								uni.setStorageSync("nickname", that.username);
								uni.setStorageSync("nowTable", `${that.optionsValues[that.index]}`);
								res = await that.$api.session(`${that.optionsValues[that.index]}`);
								if (res.data.touxiang) {
									uni.setStorageSync('headportrait', res.data.touxiang);
								} else if (res.data.headportrait) {
									uni.setStorageSync('headportrait', res.data.headportrait);
								}
								uni.setStorageSync('userSession',JSON.stringify(res.data))
								// 保存用户id
								uni.setStorageSync("appUserid", res.data.id);
								if (res.data.vip) {
									uni.setStorageSync("vip", res.data.vip);
								}
								uni.setStorageSync("appRole", `${that.options[that.index]}`);
								that.$utils.tab('../index/index');
							}
						}
					})
					
				}
			},
			// #endif
			styleChange() {
				this.$nextTick(()=>{
					// document.querySelectorAll('.uni-input .uni-input-input').forEach(el=>{
					//   el.style.backgroundColor = this.loginFrom.content.input.backgroundColor
					// })
				})
			},
			onRegisterTap(tableName) {
                uni.setStorageSync("loginTable", tableName);
				this.$utils.jump('../register/register')
			},
			async onLoginTap() {
                if (!this.username) {
					this.$utils.msg('请输入用户名')
					return
				}
                if (!this.password) {
					this.$utils.msg('请输入用户密码')
					return
				}
                if (!this.optionsValues[this.index]) {
					this.$utils.msg('请选择登录用户类型')
					return
				}

				this.loginPost()

			},
			async loginPost() {
				
				let res = await this.$api.login(`${this.optionsValues[this.index]}`, {
					username: this.username,
					password: this.password
				});
				uni.removeStorageSync("useridTag");
				uni.setStorageSync("appToken", res.token);
				uni.setStorageSync("nickname",this.username);
				uni.setStorageSync("nowTable", `${this.optionsValues[this.index]}`);
				res = await this.$api.session(`${this.optionsValues[this.index]}`);
				if(res.data.touxiang) {
				    uni.setStorageSync('headportrait', res.data.touxiang);
				} else if(res.data.headportrait) {
				    uni.setStorageSync('headportrait', res.data.headportrait);
				}
				uni.setStorageSync('userSession',JSON.stringify(res.data))
				// 保存用户id
				uni.setStorageSync("appUserid", res.data.id);
				if(res.data.vip) {
					uni.setStorageSync("vip", res.data.vip);
				}
				uni.setStorageSync("appRole", `${this.options[this.index]}`);
				this.$utils.tab('../index/index');
			},
			optionsChange(e) {
				this.index = e.target.value
			}
		}
	}
</script>

<style lang="scss" scoped>
	page {
		height: 100%;
	}
	
	.content {
		height: 100%;
		box-sizing: border-box;
	}
	
</style>
