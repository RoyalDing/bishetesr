<template>
<view class="content">
	<view :style='{"alignContent":"flex-start","padding":"48rpx 24rpx 0","borderColor":"#c0c0c0","alignItems":"flex-start","flexWrap":"wrap","background":"#fff","borderWidth":"2rpx 0 0 0","display":"flex","width":"100%","borderStyle":"solid","height":"auto"}'>
		<form :style='{"width":"100%","padding":"0","background":"none","display":"block","height":"auto"}'>
			<view :style='{"padding":"4rpx 40rpx","margin":"0 0 40rpx 0","borderColor":"#b0cb5e","alignItems":"center","borderRadius":"8rpx","borderWidth":"2rpx","background":"#f8fff7","display":"flex","width":"100%","borderStyle":"solid","height":"auto"}'>
				<xia-editor :style='{"minHeight":"300rpx","padding":"10rpx 0","margin":"0px","color":"#666","flex":"1","background":"rgba(255, 255, 255, 0)","width":"100%","fontSize":"28rpx","height":"auto"}' v-model="content" @editorChange="contentChange" placeholder="回复"></xia-editor>
			</view>
			<view :style='{"width":"100%","padding":"0","margin":"40rpx 0 0","justifyContent":"center","display":"flex","height":"auto"}'>
				<button :style='{"border":"0","padding":"0px","margin":"0 0px","color":"rgb(255, 255, 255)","borderRadius":"16rpx","background":"linear-gradient(30deg, rgba(238,230,164,1) 0%, rgba(181,205,99,1) 100%)","width":"100%","lineHeight":"88rpx","fontSize":"32rpx","height":"88rpx"}' @tap="onReplyTap" class="bg-red margin-tb-sm">提交回复</button>
			</view>
		</form>
	</view>
</view>
</template>

<script>
	import xiaEditor from '@/components/xia-editor/xia-editor'
	export default {
		data() {
			return {
				pid: '',
				content: '',
				username: '',
				avatarurl: '',
				user: {},
				sensitiveWordsArr: [],
			}
		},
		components: {
			xiaEditor
		},
		async onLoad(options) {
			this.pid = options.pid;
			let table = uni.getStorageSync("nowTable");
			// 获取用户信息
			let res = await this.$api.session(table);
			this.user = res.data;
			if(table == `yonghu`){
				this.username = this.user.yonghuzhanghao
			}
			if(table == `congyezhe`){
				this.username = this.user.peiwanzhanghao
			}
			let senArr = await this.$api.info('sensitivewords',1)
			this.sensitiveWordsArr = senArr.data.content.split(',')
		},
		methods: {
			contentChange(e) {
				this.content = e
			},
			async onReplyTap() {
				if(this.content==''){
					this.$utils.msg('内容不能为空');
					return false
				}
				this.avatarurl = uni.getStorageSync('headportrait')?uni.getStorageSync('headportrait'):'';
				for(var i=0; i<this.sensitiveWordsArr.length; i++){
					//全局替换
					var reg = new RegExp(this.sensitiveWordsArr[i],"g");
					//判断内容中是否包括敏感词
					if (this.content.indexOf(this.sensitiveWordsArr[i]) > -1) {
						// 将敏感词替换为 **
						this.content = this.content.replace(reg,"**");
					}
				}
				
				await this.$api.save('forum',{
					parentid: this.pid,
					content: this.content,
					avatarurl: this.avatarurl,
					username: this.username,
					toptime: this.$utils.getCurDateTime()
				});
				this.$utils.msgBack('回复成功');
				uni.setStorageSync('forumComType', true);
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
