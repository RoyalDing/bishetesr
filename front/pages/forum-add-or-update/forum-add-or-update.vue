<template>
<view class="content">
	<view :style='{"alignContent":"flex-start","padding":"48rpx 24rpx 0","borderColor":"#c0c0c0","alignItems":"flex-start","flexWrap":"wrap","background":"#fff","borderWidth":"2rpx 0 0 0","display":"flex","width":"100%","borderStyle":"solid","height":"auto"}'>
		<form :style='{"width":"100%","padding":"0","background":"none","display":"block","height":"auto"}'>
			<view :style='{"padding":"4rpx 40rpx","margin":"0 0 40rpx 0","borderColor":"#b0cb5e","alignItems":"center","borderRadius":"8rpx","borderWidth":"2rpx","background":"#f8fff7","display":"flex","width":"100%","borderStyle":"solid","height":"auto"}'>
				<input :style='{"border":"0","padding":"0","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","flex":"1","background":"rgba(255, 255, 255, 0)","fontSize":"28rpx","height":"80rpx"}' v-model="forum.title" placeholder="标题"></input>
			</view>
			<view :style='{"padding":"4rpx 40rpx","margin":"0 0 40rpx 0","borderColor":"#b0cb5e","alignItems":"center","borderRadius":"8rpx","borderWidth":"2rpx","background":"#f8fff7","display":"flex","width":"100%","borderStyle":"solid","height":"auto"}'>
				<picker :style='{"width":"100%","flex":"1","height":"auto"}' @change="setIsDoneTap" :value="index" :range="options">
					<view class="uni-picker-type" :style='{"width":"100%","lineHeight":"80rpx","fontSize":"28rpx","color":"#b0cb5e"}'>{{options[index]}}</view>
				</picker>
			</view>
			<view :style='{"padding":"4rpx 40rpx","margin":"0 0 40rpx 0","borderColor":"#b0cb5e","alignItems":"center","borderRadius":"8rpx","borderWidth":"2rpx","background":"#f8fff7","display":"flex","width":"100%","borderStyle":"solid","height":"auto"}'>
				<picker :style='{"width":"100%","flex":"1","height":"auto"}' @change="setIsanonTap" :value="index2" :range="options2">
					<view class="uni-picker-type" :style='{"width":"100%","lineHeight":"80rpx","fontSize":"28rpx","color":"#b0cb5e"}'>{{options2[index2]}}</view>
				</picker>
			</view>
			<view :style='{"padding":"4rpx 40rpx","margin":"0 0 40rpx 0","borderColor":"#b0cb5e","alignItems":"center","borderRadius":"8rpx","borderWidth":"2rpx","background":"#f8fff7","display":"flex","width":"100%","borderStyle":"solid","height":"auto"}'>
				<picker :style='{"width":"100%","flex":"1","height":"auto"}' @change="setCategoryTap" :value="categoryIndex" range-key="typename" :range="categoryList">
					<view class="uni-picker-type" :style='{"width":"100%","lineHeight":"80rpx","fontSize":"28rpx","color":"#b0cb5e"}'>{{categoryList[categoryIndex].typename}}</view>
				</picker>
			</view>
			<view style="display: flex;align-items: center;padding: 10px 0;">
				<image @click="imgView(item,index)" v-for="(item,index) in picList" :key="index" :src="baseUrl + item" style="width: 50px;margin: 0 5px 0 0;" mode="widthFix"></image>
				<view style="padding: 0 10px;line-height: 20px;background: #ccc;color: #333;" @click="uploadImg">上传图片</view>
			</view>
			<view :style='{"padding":"4rpx 40rpx","margin":"0 0 40rpx 0","borderColor":"#b0cb5e","alignItems":"center","borderRadius":"8rpx","borderWidth":"2rpx","background":"#f8fff7","display":"flex","width":"100%","borderStyle":"solid","height":"auto"}'>
				<xia-editor :style='{"minHeight":"300rpx","padding":"10rpx 0","margin":"0px","color":"#666","flex":"1","background":"rgba(255, 255, 255, 0)","width":"100%","fontSize":"28rpx","height":"auto"}' v-model="forum.content" @editorChange="contentChange" placeholder="内容"></xia-editor>
			</view>
			<view :style='{"width":"100%","padding":"0","margin":"40rpx 0 0","justifyContent":"center","display":"flex","height":"auto"}'>
				<button :style='{"border":"0","padding":"0px","margin":"0 0px","color":"rgb(255, 255, 255)","borderRadius":"16rpx","background":"linear-gradient(30deg, rgba(238,230,164,1) 0%, rgba(181,205,99,1) 100%)","width":"100%","lineHeight":"88rpx","fontSize":"32rpx","height":"88rpx"}' @tap="onSubmitTap" class="bg-red margin-tb-sm">确认提交</button>
			</view>
		</form>
	</view>
</view>
</template>

<script>
	import xiaEditor from '@/components/xia-editor/xia-editor';
	export default {
		data() {
			return {
				forum: {
					content: '',
					id: '',
					title: '',
					isdone: '开放',
					parentid: 0,
					typename: '',
					isanon: 0,
					cover: ''
				},
				picList: [],
				index: 0,
				options: ['开放', '关闭'],
				index2: 0,
				options2: ['实名', '匿名'],
				categoryIndex: 0,
				categoryList: [],
				username: '',
				user: {},
				sensitiveWordsArr: [],
			}
		},
		components: {
			xiaEditor
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
			if(table == `yonghu`){
				this.username = this.user.yonghuzhanghao
			}
			if(table == `congyezhe`){
				this.username = this.user.peiwanzhanghao
			}
			if(this.userid) {
				res = await this.$api.page('forumtype', {page:1,limit:100});
			} else {
				res = await this.$api.list('forumtype', {page:1,limit:100});
			}
			this.forum.typename = res.data.list[0].typename
			this.categoryList = res.data.list;
			if (options.id) {
				this.id = options.id;
				let res = await this.$api.info('forum',this.id);
				this.forum = res.data
			}
			this.styleChange()
			let senArr = await this.$api.info('sensitivewords',1)
			this.sensitiveWordsArr = senArr.data.content.split(',')
		},
		methods: {
			imgView(url,index){
				let that = this
				uni.showActionSheet({
					itemList: ['预览','删除'],
					success(res) {
						if(res.tapIndex==0){
							let arr = []
							for(let x in that.picList){
								arr.push(that.baseUrl + that.picList[x])
							}
							uni.previewImage({
								current: that.baseUrl + url,
								urls: arr
							})
						}else if(res.tapIndex==1){
							that.picList.splice(index,1)
						}
					}
				})
			},
			async uploadImg(){
				let _this = this;
				await this.$api.upload(function(res) {
					_this.picList.push('upload/' + res.file)
					_this.$forceUpdate();
				});
			},
			contentChange(e) {
				this.forum.content = e
			},
			styleChange() {
				this.$nextTick(()=>{
					// document.querySelectorAll('.my-publish-pv .uni-input-input').forEach(el=>{
					//   el.style.backgroundColor = this.myPublishForm.content.input.backgroundColor
					// })
				})
			},
			async onSubmitTap() {
				if(this.forum.title==''){
					this.$utils.msg('标题不能为空');
					return false
				}
				if(this.forum.content==''){
					this.$utils.msg('内容不能为空');
					return false
				}
				if(this.picList.length){
					this.forum.cover = this.picList.join(',')
				}
				this.forum.username = this.username;
				for(var i=0; i<this.sensitiveWordsArr.length; i++){
					//全局替换
					var reg = new RegExp(this.sensitiveWordsArr[i],"g");
					//判断内容中是否包括敏感词
					if (this.forum.content.indexOf(this.sensitiveWordsArr[i]) > -1) {
						// 将敏感词替换为 **
						this.forum.content = this.forum.content.replace(reg,"**");
					}
				}
				if (this.id) {
					await this.$api.update('forum',this.forum);
				} else {
					this.forum.toptime = this.$utils.getCurDateTime()
					await this.$api.save('forum',this.forum);
				}
				this.$utils.msgBack('操作成功');
			},
			setIsDoneTap(e) {
				// this.forum.isdone = e;
				this.index = e.target.value
				this.forum.isdone = this.options[this.index]
				_this.$forceUpdate();
			},
			setIsanonTap(e){
				this.index2 = e.target.value
				this.forum.isanon = this.index2
				_this.$forceUpdate();
			},
			setCategoryTap(e){
				this.categoryIndex = e.target.value
				this.forum.typename = this.categoryList[this.categoryIndex].typename
				_this.$forceUpdate();
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
