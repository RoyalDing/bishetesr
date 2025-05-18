<template>
<view class="content">
	<view :style='{"alignContent":"flex-start","padding":"48rpx 24rpx 0","borderColor":"#c0c0c0","alignItems":"flex-start","flexWrap":"wrap","background":"#fff","borderWidth":"2rpx 0 0 0","display":"flex","width":"100%","borderStyle":"solid","height":"auto"}'>
		<form :style='{"width":"100%","padding":"0","background":"none","display":"block","height":"auto"}'>
			<view :style='{"padding":"4rpx 40rpx","margin":"0 0 40rpx 0","borderColor":"#b0cb5e","alignItems":"center","borderRadius":"8rpx","borderWidth":"2rpx","background":"#f8fff7","display":"flex","width":"100%","borderStyle":"solid","height":"auto"}'>
				<input :style='{"border":"0","padding":"0","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","flex":"1","background":"rgba(255, 255, 255, 0)","fontSize":"28rpx","height":"80rpx"}' disabled="true" v-model="ruleForm.username" placeholder="留言人用户名"></input>
			</view>
			<view :style='{"padding":"4rpx 40rpx","margin":"0 0 40rpx 0","borderColor":"#b0cb5e","alignItems":"center","borderRadius":"8rpx","borderWidth":"2rpx","background":"#f8fff7","display":"flex","width":"100%","borderStyle":"solid","height":"auto"}'>
				<textarea :style='{"border":"2rpx solid #b0cb5e","padding":"24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"28rpx","height":"300rpx"}' v-model="ruleForm.content" placeholder="留言内容"></textarea>
			</view>
			<view @tap="uploadTap" :style='{"padding":"4rpx 40rpx","margin":"0 0 40rpx 0","borderColor":"#b0cb5e","alignItems":"center","borderRadius":"8rpx","borderWidth":"2rpx","background":"#f8fff7","display":"flex","width":"100%","borderStyle":"solid","height":"auto"}'>
				<image :style='{"width":"80rpx","borderRadius":"100%","objectFit":"cover","display":"block","height":"80rpx"}' class="avator" v-if="ruleForm.cpicture" :src="baseUrl+ruleForm.cpicture" mode="aspectFill"></image>
				<image :style='{"width":"80rpx","borderRadius":"100%","objectFit":"cover","display":"block","height":"80rpx"}' class="avator" v-else src="../../static/gen/upload.png" mode="aspectFill"></image>
			</view>
			<view :style='{"width":"100%","padding":"0","margin":"40rpx 0 0","justifyContent":"center","display":"flex","height":"auto"}'>
				<button :style='{"border":"0","padding":"0px","margin":"0 0px","color":"rgb(255, 255, 255)","borderRadius":"16rpx","background":"linear-gradient(30deg, rgba(238,230,164,1) 0%, rgba(181,205,99,1) 100%)","width":"100%","lineHeight":"88rpx","fontSize":"32rpx","height":"88rpx"}' @tap="onSubmitTap" class="bg-red margin-tb-sm">提交</button>
			</view>
		</form>
	</view>
</view>
</template>

<script>
	export default {
		data() {
			return {
				ruleForm: {
					userid: '',
					username: '',
					content: '',
					reply: '',
					cpicture: '',
				},
				user: {},
				sensitiveWordsArr: [],
			}
		},
		computed: {
			baseUrl() {
				return this.$base.url;
			}
		},
		async onLoad(options) {
			let table = uni.getStorageSync("nowTable");
			// 获取用户信息
			let res = await this.$api.session(table);
			this.user = res.data;
			// 如果有登录，获取登录后保存的userid
			this.ruleForm.userid = uni.getStorageSync("appUserid")
			if(table == `yonghu`){
				this.ruleForm.username = this.user.yonghuzhanghao
			}
			if(table == `congyezhe`){
				this.ruleForm.username = this.user.peiwanzhanghao
			}
			let senArr = await this.$api.info('sensitivewords',1)
			this.sensitiveWordsArr = senArr.data.content.split(',')
		},
		methods: {
			uploadTap() {
				let _this = this;
				this.$api.upload(function(res) {
					_this.ruleForm.cpicture = 'upload/' + res.file;
					_this.$forceUpdate();
				});
			},
			async onSubmitTap() {
				if(this.ruleForm.content){
					this.ruleForm.avatarurl = uni.getStorageSync('headportrait')?uni.getStorageSync('headportrait'):'';
					for(var i=0; i<this.sensitiveWordsArr.length; i++){
						//全局替换
						var reg = new RegExp(this.sensitiveWordsArr[i],"g");
						//判断内容中是否包括敏感词
						if (this.ruleForm.content.indexOf(this.sensitiveWordsArr[i]) > -1) {
							// 将敏感词替换为 **
							this.ruleForm.content = this.ruleForm.content.replace(reg,"**");
						}
					}
					await this.$api.add(`messages`, this.ruleForm);
					this.$utils.msgBack('提交成功');
				}else{
					this.$utils.msg("请填写留言内容")
				}
			}
		}
	}
</script>

<style lang="scss" scoped>
	.content {
		min-height: calc(100vh - 44px);
		box-sizing: border-box;
	}
</style>
