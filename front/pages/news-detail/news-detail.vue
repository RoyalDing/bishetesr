<template>
	<view :style='{"alignContent":"flex-start","padding":"0","borderColor":"#c0c0c0","alignItems":"flex-start","flexWrap":"wrap","background":"#fff","borderWidth":"2rpx 0 0 0","display":"flex","width":"100%","borderStyle":"solid","height":"auto"}'>
		<view class="title" :style='{"padding":"0","margin":"0","color":"#000","borderRadius":"20rpx 20rpx 0 0","textAlign":"center","background":"#ffffff","width":"100%","lineHeight":"80rpx","fontSize":"32rpx"}'>{{detail.title}}</view>
		
		<view :style='{"alignItems":"center","color":"#999","flexWrap":"wrap","background":"#ffffff","display":"flex","width":"100%","fontSize":"28rpx","justifyContent":"center"}'>
		  <view :style='{"width":"100%","padding":"0 20rpx","margin":"0px 0","textAlign":"center","order":"2"}'>
		    <text class="icon iconfont icon-shijian21" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"inherit","color":"inherit"}'></text>
		    <text :style='{"color":"inherit","lineHeight":"1.5","fontSize":"inherit"}'>发布时间：{{detail.addtime}}</text>
		  </view>
		  <view :style='{"padding":"0","margin":"0 20rpx 0 0"}'>
		    <text class="icon iconfont icon-geren16" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"inherit","color":"inherit"}'></text>
		    <text :style='{"color":"inherit","lineHeight":"1.5","fontSize":"inherit"}'>{{detail.name}}</text>
		  </view>
		  <view :style='{"padding":"0","margin":"0 20rpx 0 0"}'>
		    <text class="icon iconfont icon-zan10" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"inherit","color":"inherit"}'></text>
		    <text :style='{"color":"inherit","lineHeight":"1.5","fontSize":"inherit"}'>{{detail.thumbsupnum}}</text>
		  </view>
		  <view :style='{"padding":"0","margin":"0 20rpx 0 0"}'>
		    <text class="icon iconfont icon-shoucang10" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"inherit","color":"inherit"}'></text>
		    <text :style='{"color":"inherit","lineHeight":"1.5","fontSize":"inheritx"}'>{{detail.storeupnum}}</text>
		  </view>
		  <view :style='{"padding":"0"}'>
		    <text class="icon iconfont icon-chakan2" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"inherit","color":"inherit"}'></text>
		    <text :style='{"color":"inherit","lineHeight":"1.5","fontSize":"inherit"}'>{{detail.clicknum}}</text>
		  </view>
		</view>
		
		<view :style='{"padding":"0 24rpx","margin":"0px auto 20rpx","background":"#fff","display":"flex","width":"100%","justifyContent":"space-between","order":"4"}'>
		  <view :style='{"width":"50%","padding":"16rpx 50rpx","borderRadius":"0","background":"#b0cb5e","justifyContent":"center","display":"flex"}' @click="likeClick">
		    <text class="icon iconfont" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"30rpx","color":"#fff","order":"2"}' :class="likeType?'icon-zan10':'icon-zan10'"></text>
		    <text :style='{"margin":"0 10rpx 0 0","lineHeight":"1.5","fontSize":"30rpx","color":"#fff"}'>{{likeType?'已':''}}赞</text>
		  </view>
		  <view :style='{"width":"50%","padding":"16rpx 50rpx","borderRadius":"0","background":"#8fb9e9","justifyContent":"center","display":"flex"}' @click="collectClick">
		    <text class="icon iconfont" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"28rpx","color":"#fff","order":"2"}' :class="collectType?'icon-shoucang10':'icon-shoucang10'"></text>
		    <text :style='{"margin":"0 10rpx 0 0","lineHeight":"1.5","fontSize":"28rpx","color":"#fff"}'>{{collectType?'已':''}}收藏</text>
		  </view>
		</view>
		
		<view class="content" :style='{"border":"0px solid #ddd","padding":"24rpx","margin":"0","background":"#fff","width":"100%","lineHeight":"1.5","height":"auto"}'>
			<rich-text :nodes="detail.content"></rich-text>
		</view>
		
		<div :style='{"padding":"0 24rpx","margin":"0px auto","borderRadius":"0px","flexWrap":"wrap","background":"#fff","display":"flex","width":"100%","justifyContent":"space-between","height":"auto","order":"6"}'>
		  <div @click="prepDetailClick" :style='{"padding":"0 20rpx","margin":"0 0 20rpx 0","color":"#333","borderRadius":"0","textAlign":"center","background":"#daeaee","width":"100%","lineHeight":"72rpx","fontSize":"28rpx"}'>上一篇：prev</div>
		  <div @click="nextDetailClick" :style='{"padding":"0 20rpx","color":"#fff","borderRadius":"0","textAlign":"center","background":"#b0cb5e","width":"100%","lineHeight":"72rpx","fontSize":"28rpx"}'>下一篇：next</div>
		</div>
		
		<view class="time-content" :style='{"width":"100%","padding":"0","margin":"48rpx 0 0 0","height":"auto","order":"8"}'>
			<view class="comoment-header" :style='{"border":"2rpx solid #b0cb5e","padding":"0 0px","margin":"0 auto 40rpx","borderRadius":"60rpx","background":"none","display":"flex","width":"calc(100% - 48rpx)","justifyContent":"space-between","height":"auto"}'>
				<view :style='{"padding":"0 0 0 40rpx","color":"#333","borderRadius":"60rpx","background":"#fff","flex":"1","lineHeight":"88rpx","fontSize":"32rpx"}'>评论</view>
				<view :style='{"padding":"0 30rpx","margin":"0 0 0 20rpx","borderRadius":"60rpx","background":"linear-gradient(30deg, rgba(238,230,164,1) 0%, rgba(181,205,99,1) 100%)","display":"flex"}' @click="onCommentTap" class="btn-comment-content" style="display: flex;align-items: center;">
					<text class="icon iconfont icon-tianjia14" :style='{"margin":"0 8rpx 0 0","lineHeight":"88rpx","fontSize":"28rpx","color":"#fff","display":"none","order":"2"}'></text>
					<text :style='{"margin":"0 10rpx 0 0","lineHeight":"88rpx","fontSize":"30rpx","color":"#fff"}'>添加评论</text>
				</view>
			</view>
			<view :style='{"border":"2rpx solid #b0cb5e","padding":"24rpx","margin":"24rpx auto 0","borderRadius":"40rpx","background":"#f8fff7","width":"calc(100% - 48rpx)","position":"relative","height":"auto"}' v-for="(item,index) in commentList" v-bind:key="index" class="cu-item comment-item">
				<view :style='{"width":"100%","alignItems":"center","display":"flex","height":"auto"}'>
					<image :style='{"width":"76rpx","margin":"0 8rpx 0 0","borderRadius":"100%","display":"block","height":"76rpx"}' v-if="item.avatarurl" mode="aspectFill" :src="baseUrl+item.avatarurl"></image>
					<view :style='{"color":"#333","lineHeight":"60rpx","fontSize":"32rpx"}' class="text-grey">{{item.nickname}}</view>
				</view>
				<view :style='{"padding":"0 40rpx 0 80rpx","margin":"8rpx 0","lineHeight":"48rpx","fontSize":"30rpx","color":"#333"}' v-html="item.content"></view>
				<view :style='{"padding":"0 20rpx 0 80rpx","color":"#999","top":"40rpx","textAlign":"left","lineHeight":"48rpx","fontSize":"26rpx","position":"absolute","right":"20rpx"}'>{{item.addtime}}</view>
				<view v-if="item.reply" :style='{"padding":"0 40rpx 0 80rpx","margin":"8rpx 0","lineHeight":"48rpx","fontSize":"30rpx","color":"#333"}' class="text-gray text-content text-df">
					回复:<view v-html="item.reply"></view>
				</view>
				<view style="display: flex;display: flex;justify-content: flex-end;padding: 6rpx 0;" v-if="userid==item.userid">
					<view style="color: #999;font-size: 16rpx;" @click="delClick(item.id)">删除</view>
				</view>
			</view>
		</view>

		<!-- 热门 -->
		<view class="hot" :style='{"width":"calc(100% - 48rpx)","margin":"40rpx auto 0","background":"none","height":"auto","order":"10"}'>
		  <view :style='{"padding":"0 0 0 20rpx","margin":"0","borderColor":"#23baf7","color":"#fff","textAlign":"left","background":"url(http://codegen.caihongy.cn/20241123/660fac4a1f6741a0a62b0c05d5fd6f30.png) no-repeat right center / auto 100%,url(http://codegen.caihongy.cn/20241123/64eaed6349684230932b0df60dfde52c.png) no-repeat left center / 100% 100%","borderWidth":"0 0 0 0px","width":"100%","lineHeight":"120rpx","fontSize":"32rpx","position":"relative","borderStyle":"solid","fontWeight":"600"}'>热门信息</view>
		  <view :style='{"padding":"0","margin":"20rpx 0 0","borderRadius":"20rpx","flexWrap":"wrap","background":"none","display":"flex","width":"100%","justifyContent":"space-between","height":"auto"}'>
		    <view v-for="(item,index) in hotList" :key="index" :style='{"border":"0px solid #174add60","padding":"12rpx","margin":"0 0 40rpx","borderRadius":"0px","flexWrap":"wrap","background":"linear-gradient(270.00deg, rgb(189, 230, 243),rgb(238, 230, 164) 97.532%)","display":"flex","width":"48%","height":"auto"}' @click="toDetail(item.id)">
			  <image :style='{"margin":"0 0 12rpx 0","objectFit":"cover","borderRadius":"0px","display":"block","width":"100%","height":"200rpx","order":"-1"}' mode="aspectFill" :src="baseUrl + item.picture"></image>
		      <view :style='{"padding":"0 8rpx","overflow":"hidden","whiteSpace":"nowrap","color":"#224366","background":"#fff","width":"100%","lineHeight":"48rpx","fontSize":"28rpx","textOverflow":"ellipsis","order":"-1"}'>{{ item.title }}</view>
		      <view :style='{"padding":"0 8rpx","color":"#999","textAlign":"center","display":"none","width":"100%","lineHeight":"48rpx","fontSize":"28rpx"}'>{{ item.addtime }}</view>
		    </view>
		  </view>
		</view>
		<!-- 推荐 -->
		<view class="recommend" :style='{"width":"calc(100% - 48rpx)","margin":"0px auto 0","background":"none","height":"auto","order":"12"}'>
		  <view :style='{"padding":"0px","margin":"0 0 40rpx","borderColor":"#23baf7","color":"#B0CB5E","textAlign":"left","background":"url(http://codegen.caihongy.cn/20241123/718dc8bbcb6441929f2293e30cf62f81.png) no-repeat right bottom / 80%","borderWidth":"0 0 0 0px","width":"100%","fontSize":"36rpx","lineHeight":"80rpx","position":"relative","borderStyle":"solid","fontWeight":"600"}'>最新推荐</view>
		  <view :style='{"padding":"0","borderRadius":"20rpx","flexWrap":"wrap","background":"none","display":"flex","width":"100%","justifyContent":"space-between","height":"auto"}'>
		    <view v-for="(item,index) in recommendList" :key="index" :style='{"border":"0px solid #174add60","padding":"12rpx","margin":"0 0 40rpx","borderRadius":"0px","flexWrap":"wrap","background":"linear-gradient(270.00deg, rgb(189, 230, 243),rgb(238, 230, 164) 97.532%)","display":"flex","width":"48%","height":"auto"}' @click="toDetail(item.id)">
		      <image :style='{"width":"40%","margin":"0","objectFit":"cover","borderRadius":"0px","display":"block","height":"96rpx"}' mode="aspectFill" :src="baseUrl + item.picture"></image>
			  <view :style='{"padding":"0 8rpx","overflow":"hidden","color":"#333","maxHeight":"96rpx","background":"#fff","width":"calc(60% - 0px)","lineHeight":"48rpx","fontSize":"28rpx","order":"2"}'>{{ item.title }}</view>
		      <view :style='{"padding":"0 8rpx","color":"#999","textAlign":"center","display":"none","width":"calc(100% - 0px)","lineHeight":"48rpx","fontSize":"26rpx"}'>{{ item.addtime }}</view>
		    </view>
		  </view>
		</view>

	</view>
</template>
<script>
	export default {
		data() {
			return {
				detail: {},
				id: '',
				likeType: false,
				likeForm: {},
				collectType: false,
				collectForm: {},
				commentList: [],
				page: 1,
				allList: [],
				currentIndex: 0,
				hotList: [],
				recommendList: [],
			}
		},
		async onLoad(options) {
			this.id = options.id;
			this.getInfo()
			
			this.getHotList()
			this.getRecommendList()
		},
		onShow() {
			let cleanType = uni.getStorageSync('discussnewsCleanType')
			if(cleanType){
				uni.removeStorageSync('discussnewsCleanType')
				this.page = 1
				this.commentList = []
				this.getCommentList()
			}
		},
		onReachBottom() {
			this.page++
			this.getCommentList()
		},
		computed:{
			baseUrl() {
				return this.$base.url;
			},
			userid(){
				return uni.getStorageSync('appUserid')
			}
		},
		methods: {
			async getInfo(){
				let res = await this.$api.info('news', this.id)
				res.data.content = res.data.content.replace(/<img/g,'<img style="width: 100%;"');
				this.detail = res.data;
				uni.pageScrollTo({
					scrollTop: 0,
					duration: 100,
				})
				this.getLike()
				this.getCollect()
				this.getCommentList()
				res = await this.$api.list('news',{page:1,limit:100,sort:'addtime',order:'desc'})
				for(let x in res.data.list){
					if(res.data.list[x].id == this.id){
						this.currentIndex = Number(x)
						break
					}
				}
				this.allList = res.data.list
				
			},
			// 获取点赞状态
			async getLike() {
				let res = await this.$api.list('storeup', {
					page: 1,
					limit: 1,
					type: '21',
					userid: uni.getStorageSync('appUserid'),
					refid: this.id,
					tablename: 'news'
				})
				if (res.data.list.length) {
					this.likeType = true
					this.likeForm = res.data.list[0]
				} else {
					this.likeType = false
					this.likeForm = {}
				}
			},
			// 获取热门列表
			async getHotList(){
				let res = await this.$api.recommend('news',{page:1, limit: 4,sort:'addtime',order:'desc'})
				this.hotList = res.data.list;
			},
			// 获取推荐列表	
			async getRecommendList(){
				let res;
				if(uni.getStorageSync("appUserid")){
					res = await this.$api.recommend2('news',{page:1, limit: 4,sort:'addtime',order:'desc'})
				}else{
					res = await this.$api.recommend('news',{page:1, limit: 4,sort:'addtime',order:'desc'})
				}
				
				this.recommendList = res.data.list;
			},
			// 上一篇
			prepDetailClick(){
				if(this.currentIndex == 0){
					this.$message.error('已经是第一篇了')
					return false
				}
				this.currentIndex--
				this.id = this.allList[this.currentIndex].id
				this.page = 1
				this.getInfo()
			},
			// 下一篇
			nextDetailClick(){
				if(this.currentIndex == this.allList.length - 1){
					this.$message.error('已经是最后一篇了')
					return false
				}
				this.currentIndex++
				this.id = this.allList[this.currentIndex].id
				this.page = 1
				this.getInfo()
			},
			toDetail(id){
				this.id = id
				this.getInfo()
			},
			// 获取收藏状态
			async getCollect() {
				let res = await this.$api.list('storeup', {
					page: 1,
					limit: 1,
					type: '1',
					userid: uni.getStorageSync('appUserid'),
					refid: this.id,
					tablename: 'news'
				})
				if (res.data.list.length) {
					this.collectType = true
					this.collectForm = res.data.list[0]
				} else {
					this.collectType = false
					this.collectForm = {}
				}
			},
			// 点赞按钮
			async likeClick() {
				let that = this
				if (this.likeType) {
					uni.showModal({
						title: '提示',
						content: '是否取消点赞？',
						async success(res) {
							if (res.confirm) {
								await that.$api.del('storeup', JSON.stringify([that.likeForm.id]))
								that.$utils.msg('取消成功')
								that.detail.thumbsupnum--
								await that.$api.update('news', that.detail)
								that.getLike()
							}
						}
					})
				} else {
					await that.$api.add('storeup', {
						userid: uni.getStorageSync('appUserid'),
						refid: this.id,
						type: '21',
						name: this.detail.title,
						picture: this.detail.picture,
						tablename: 'news',
					})
					this.$utils.msg('点赞成功')
					that.detail.thumbsupnum++
					await that.$api.update('news', that.detail)
					this.getLike()
				}
			},
			// 收藏按钮
			async collectClick() {
				let that = this
				if (this.collectType) {
					uni.showModal({
						title: '提示',
						content: '是否取消收藏？',
						async success(res) {
							if (res.confirm) {
								await that.$api.del('storeup', JSON.stringify([that.collectForm.id]))
								that.$utils.msg('取消成功')
								that.detail.storeupnum--
								await that.$api.update('news', that.detail)
								that.getCollect()
							}
						}
					})
				} else {
					await that.$api.add('storeup', {
						userid: uni.getStorageSync('appUserid'),
						refid: this.id,
						type: '1',
						name: this.detail.title,
						picture: this.detail.picture,
						tablename: 'news',
					})
					this.$utils.msg('收藏成功')
					that.detail.storeupnum++
					await that.$api.update('news', that.detail)
					this.getCollect()
				}
			},
			// 获取评论列表
			async getCommentList() {
				if(this.page == 1){
					this.commentList = []
				}
				let res = await this.$api.list('discussnews', {
					page: this.page,
					limit: 10,
					refid: this.id
				});
				if(res.data.list.length==0){
					this.page--
				}
				this.commentList = this.commentList.concat(res.data.list)
			},
			// 跳转新增评论
			async onCommentTap() {
				this.$utils.jump(`../discussnews/add-or-update?refid=${this.id}`)
			},
			// 删除当前评论
			delClick(id) {
				let that = this
				uni.showModal({
					title: '提示',
					content: '是否删除此评论？',
					async success(res) {
						if (res.confirm) {
							await that.$api.del('discussnews', JSON.stringify([id]))
							that.$utils.msg('删除成功')
							setTimeout(() => {
								that.page = 1
								that.commentList = []
								that.getCommentList()
							}, 1500)
						}
					}
				})
			},
		}
	}
</script>

<style scoped lang="scss">
	page {
		background: #FFFFFF;
	}
</style>
