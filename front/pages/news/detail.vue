
<template>
<view>
<mescroll-uni @init="mescrollInit" :up="upOption" :down="downOption" @down="downCallback" @up="upCallback">
	<view class="content">
		<view class="container" :style='{"alignContent":"flex-start","padding":"0","borderColor":"#c0c0c0","alignItems":"flex-start","flexWrap":"wrap","background":"#fff","borderWidth":"2rpx 0 0 0","display":"flex","width":"100%","borderStyle":"solid","height":"auto"}'>
			<view :style='{"alignContent":"flex-start","padding":"0","margin":"0 auto","flexWrap":"wrap","background":"linear-gradient(135.00deg, rgb(238, 230, 164) 0.464%,rgb(215, 237, 239) 100%)","display":"flex","width":"100%","position":"relative","height":"auto","zIndex":"9"}' class="detail-content">
				<view :style='{"padding":"0","margin":"20rpx auto 0","borderColor":"#ccc","display":"flex","justifyContent":"flex-end","borderRadius":"0","flexWrap":"wrap","borderWidth":"0 0 2rpx 0","background":"url(http://codegen.caihongy.cn/20241125/bac517a573234e11a6f4c8f720a6aedc.png) no-repeat center top / 100% auto","width":"calc(100% - 48rpx)","position":"relative","borderStyle":"solid","height":"80rpx","zIndex":"999"}' class="detail-list-item price">
					<view :style='{"margin":"12rpx 20rpx 0 0","display":"flex"}' v-if="storeupFlag==1" @click="shoucang">
						<text class="icon iconfont icon-shoucang12" :style='{"border":"2rpx solid #ffc44160","padding":" 0 10rpx","margin":"0 0px 0 0","color":"#ffc441","borderRadius":"8rpx","background":"#ffc44120","lineHeight":"56rpx","fontSize":"32rpx","order":"2","height":"56rpx"}'></text>
						<text :style='{"margin":"0 10rpx 0 0","lineHeight":"56rpx","fontSize":"30rpx","color":"#ffc441"}'>已收藏</text>
					</view>
					<view :style='{"margin":"12rpx 20rpx 0 0","display":"flex"}' v-if="storeupFlag==0" @click="shoucang">
						<text class="icon iconfont icon-shoucang10" :style='{"border":"2rpx solid #b0cb5e50","padding":" 0 10rpx","margin":"0 0px 0 0","color":"#b0cb5e","borderRadius":"8rpx","background":"#b0cb5e10","lineHeight":"56rpx","fontSize":"32rpx","order":"2","height":"56rpx"}'></text>
						<text :style='{"margin":"0 10rpx 0 0","lineHeight":"56rpx","fontSize":"30rpx","color":"#b0cb5e"}'>收藏</text>
					</view>
				</view>


				<view class="detail-list-item" :style='{"padding":"0 24rpx","margin":"0 auto","borderColor":"#ccc","borderRadius":"0","borderWidth":"0 0 2rpx 0","background":"#fff","display":"flex","width":"calc(100% - 48rpx)","borderStyle":"solid","justifyContent":"flex-start","height":"auto"}'>
					<view class="lable" :style='{"padding":"0 20rpx 0 0","whiteSpace":"nowrap","color":"#333","textAlign":"left","width":"auto","lineHeight":"80rpx","fontSize":"28rpx"}'>标题：</view>
					<view class="text" :style='{"padding":"0px","margin":"0px","lineHeight":"80rpx","fontSize":"28rpx","color":"rgb(0, 0, 0)","flex":"1"}' >{{detail.title}}</view>
				</view>
				<view class="detail-list-item" :style='{"padding":"0 24rpx","margin":"0 auto","borderColor":"#ccc","borderRadius":"0","borderWidth":"0 0 2rpx 0","background":"#fff","display":"flex","width":"calc(100% - 48rpx)","borderStyle":"solid","justifyContent":"flex-start","height":"auto"}'>
					<view class="lable" :style='{"padding":"0 20rpx 0 0","whiteSpace":"nowrap","color":"#333","textAlign":"left","width":"auto","lineHeight":"80rpx","fontSize":"28rpx"}'>分类名称：</view>
					<view class="text" :style='{"padding":"0px","margin":"0px","lineHeight":"80rpx","fontSize":"28rpx","color":"rgb(0, 0, 0)","flex":"1"}' >{{detail.typename}}</view>
				</view>
				<view class="detail-list-item" :style='{"padding":"0 24rpx","margin":"0 auto","borderColor":"#ccc","borderRadius":"0","borderWidth":"0 0 2rpx 0","background":"#fff","display":"flex","width":"calc(100% - 48rpx)","borderStyle":"solid","justifyContent":"flex-start","height":"auto"}'>
					<view class="lable" :style='{"padding":"0 20rpx 0 0","whiteSpace":"nowrap","color":"#333","textAlign":"left","width":"auto","lineHeight":"80rpx","fontSize":"28rpx"}'>发布人：</view>
					<view class="text" :style='{"padding":"0px","margin":"0px","lineHeight":"80rpx","fontSize":"28rpx","color":"rgb(0, 0, 0)","flex":"1"}' >{{detail.name}}</view>
				</view>
				<view class="detail-list-item" :style='{"padding":"20rpx 20rpx","margin":"0 auto","borderColor":"#ccc","borderWidth":"0 0 0px 0","background":"#fff","display":"flex","width":"calc(100% - 48rpx)","borderStyle":"solid","height":"auto","order":"3"}'>
					<image :style='{"width":"80rpx","borderRadius":"100%","objectFit":"cover","display":"block","height":"80rpx"}' v-if="detail.headportrait" :src="baseUrl+detail.headportrait"></image>
				</view>
				<view class="detail-list-item" :style='{"padding":"0 24rpx","margin":"0 auto","borderColor":"#ccc","borderRadius":"0","borderWidth":"0 0 2rpx 0","background":"#fff","display":"flex","width":"calc(100% - 48rpx)","borderStyle":"solid","justifyContent":"flex-start","height":"auto"}'>
					<view class="lable" :style='{"padding":"0 20rpx 0 0","whiteSpace":"nowrap","color":"#333","textAlign":"left","width":"auto","lineHeight":"80rpx","fontSize":"28rpx"}'>点击次数：</view>
					<view class="text" :style='{"padding":"0px","margin":"0px","lineHeight":"80rpx","fontSize":"28rpx","color":"rgb(0, 0, 0)","flex":"1"}' >{{detail.clicknum}}</view>
				</view>
				<view class="detail-list-item" :style='{"padding":"0 24rpx","margin":"0 auto","borderColor":"#ccc","borderRadius":"0","borderWidth":"0 0 2rpx 0","background":"#fff","display":"flex","width":"calc(100% - 48rpx)","borderStyle":"solid","justifyContent":"flex-start","height":"auto"}'>
					<view class="lable" :style='{"padding":"0 20rpx 0 0","whiteSpace":"nowrap","color":"#333","textAlign":"left","width":"auto","lineHeight":"80rpx","fontSize":"28rpx"}'>收藏数：</view>
					<view class="text" :style='{"padding":"0px","margin":"0px","lineHeight":"80rpx","fontSize":"28rpx","color":"rgb(0, 0, 0)","flex":"1"}' >{{detail.storeupnum}}</view>
				</view>
				<view class="detail-list-item" :style='{"padding":"20rpx 20rpx","margin":"0 auto","borderColor":"#ccc","borderWidth":"0 0 0px 0","background":"#fff","display":"flex","width":"calc(100% - 48rpx)","borderStyle":"solid","height":"auto","order":"3"}'>
					<image :style='{"width":"80rpx","borderRadius":"100%","objectFit":"cover","display":"block","height":"80rpx"}' v-if="detail.picture" :src="baseUrl+detail.picture"></image>
				</view>

				<view :style='{"padding":"20rpx 20rpx","margin":"0 auto","background":"#fff","display":"flex","width":"calc(100% - 48rpx)","justifyContent":"center","order":"4"}'>
					<view :style='{"margin":"0","borderRadius":"8rpx 0 0 8rpx","color":"#fff","background":"#b0cb5e","display":"flex","width":"50%","fontSize":"30rpx","justifyContent":"center","height":"auto"}' class="detail-list-item" v-if="!thumbsupFlag&&!crazilyFlag" @tap="zan">
						<view :style='{"padding":"0 20rpx 0 0","lineHeight":"68rpx","fontSize":"inherit","color":"inherit","textAlign":"right"}' class="lable">赞</view>
						<view :style='{"color":"inherit","lineHeight":"68rpx","fontSize":"inherit"}'>{{detail.thumbsupnum}}</view>
						<view :style='{"margin":" 0 0 0 10rpx","lineHeight":"68rpx","fontSize":"inherit","color":"inherit"}' class="icon iconfont icon-zan10"></view>
					</view>
					<view :style='{"margin":"0","borderRadius":"8rpx","color":"#fff","background":"#b0cb5e","display":"flex","width":"100%","fontSize":"30rpx","justifyContent":"center","height":"auto"}' class="detail-list-item" v-if="thumbsupFlag" @tap="zan">
						<view :style='{"padding":"0 20rpx 0 0","lineHeight":"68rpx","fontSize":"inherit","color":"inherit","textAlign":"right"}' class="lable">取消赞</view>
						<view :style='{"color":"inherit","lineHeight":"68rpx","fontSize":"inherit"}'>{{detail.thumbsupnum}}</view>
						<view :style='{"margin":" 0 0 0 10rpx","lineHeight":"68rpx","fontSize":"inherit","color":"inherit"}' class="icon iconfont icon-zan10"></view>
					</view>
					<view :style='{"margin":"0","borderRadius":"0 8rpx 8rpx 0","color":"#666","background":"#8fb9e9","display":"flex","width":"50%","fontSize":"30rpx","justifyContent":"center","height":"auto"}' class="detail-list-item" v-if="!thumbsupFlag&&!crazilyFlag" @tap="cai">
						<view :style='{"padding":"0 20rpx 0 0","lineHeight":"68rpx","fontSize":"inherit","color":"inherit","textAlign":"right"}' class="lable">踩</view>
						<view :style='{"color":"inherit","lineHeight":"68rpx","fontSize":"inherit"}'>{{detail.crazilynum}}</view>
						<view :style='{"margin":" 0 0 0 10rpx","lineHeight":"68rpx","fontSize":"inherit","color":"inherit"}' class="icon iconfont icon-cai11"></view>
					</view>
					<view :style='{"margin":"0","borderRadius":"8rpx","color":"#666","background":"#8fb9e9","display":"flex","width":"100%","fontSize":"30rpx","justifyContent":"center","height":"auto"}' class="detail-list-item" v-if="crazilyFlag" @tap="cai">
						<view :style='{"padding":"0 20rpx 0 0","lineHeight":"68rpx","fontSize":"inherit","color":"inherit","textAlign":"right"}' class="lable">取消踩</view>
						<view :style='{"color":"inherit","lineHeight":"68rpx","fontSize":"inherit"}'>{{detail.crazilynum}}</view>
						<view :style='{"margin":" 0 0 0 10rpx","lineHeight":"68rpx","fontSize":"inherit","color":"inherit"}' class="icon iconfont icon-cai11"></view>
					</view>
				</view>


				<view class="detail-list-item" :style='{"padding":"0 24rpx","margin":"0 auto","borderColor":"#ccc","borderRadius":"0","borderWidth":"0 0 2rpx 0","background":"#fff","display":"flex","width":"calc(100% - 48rpx)","borderStyle":"solid","justifyContent":"flex-start","height":"auto"}'>
					<view class="lable" :style='{"padding":"0 20rpx 0 0","whiteSpace":"nowrap","color":"#333","textAlign":"left","width":"auto","lineHeight":"80rpx","fontSize":"28rpx"}'>简介：</view>
					<view class="text" :style='{"padding":"0px","margin":"0px","lineHeight":"80rpx","fontSize":"28rpx","color":"rgb(0, 0, 0)","flex":"1"}'>{{detail.introduction}}</view>
				</view>


				<view class="detail-list-item rich" :style='{"padding":"0 0 0 24rpx","margin":"0 auto","borderColor":"#ccc","borderRadius":"0","borderWidth":"0 0 2rpx 0","background":"#fff","display":"flex","width":"calc(100% - 48rpx)","borderStyle":"solid","height":"auto"}'>
					<view class="lable" :style='{"padding":"0 20rpx 0 0","whiteSpace":"nowrap","color":"#333","textAlign":"right","width":"auto","lineHeight":"80rpx","fontSize":"28rpx"}'>内容：</view>
					<view class="rich-text" :style='{"padding":"20rpx 24rpx 24rpx 0","margin":"0","lineHeight":"48rpx"}'>
						<rich-text :nodes="detail.content"></rich-text>
					</view>
				</view>


				<view class="time-content" :style='{"width":"100%","padding":"48rpx 24rpx 0","margin":"0","background":"#fff","height":"auto","order":"10"}'>
					<view class="comoment-header" :style='{"border":"2rpx solid #b0cb5e","padding":"0 0 0 20rpx","margin":"0 0 40rpx 0","borderRadius":"60rpx","background":"#f8fff7","display":"flex","width":"100%","justifyContent":"space-between","height":"auto"}'>
						<view :style='{"padding":"0 24rpx","lineHeight":"80rpx","fontSize":"32rpx","color":"#333","flex":"1"}'>评论</view>
						<view :style='{"padding":"0 30rpx","borderRadius":"60rpx","textAlign":"center","background":"linear-gradient(30deg, rgba(238,230,164,1) 0%, rgba(181,205,99,1) 100%)","display":"flex"}' @click="onCommentTap" class="btn-comment-content" style="display: flex;align-items: center;">
							<view :style='{"margin":"0 8rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#fff","display":"none","order":"2"}' class="cuIcon-add"></view>
							<view :style='{"margin":"0 10rpx 0 0","lineHeight":"80rpx","fontSize":"30rpx","color":"#fff"}'>添加评论</view>
						</view>
					</view>
				
					<view :style='{"border":"2rpx solid #b0cb5e","padding":"24rpx","margin":"24rpx 0 0 0","borderRadius":"40rpx","background":"#f8fff7","width":"100%","position":"relative","height":"auto"}' v-for="(item,index) in commentList" v-bind:key="index" class="cu-item comment-item">
						<view :style='{"position":"absolute","right":"20rpx","top":"32rpx","background":"none"}' v-if="item.istop">
							<span class="icon iconfont icon-jiantou24" :style='{"color":"#666","fontSize":"40rpx"}'></span>
						</view>
						<view :style='{"width":"100%","alignItems":"center","display":"flex","height":"auto"}'>
							<image :style='{"width":"76rpx","margin":"0 8rpx 0 0","borderRadius":"100%","display":"block","height":"76rpx"}' v-if="item.avatarurl" mode="aspectFill" :src="baseUrl+item.avatarurl"></image>
							<view :style='{"color":"#333","lineHeight":"60rpx","fontSize":"32rpx"}' class="text-grey">{{item.nickname}}</view>
						</view>
						<view :style='{"margin":"8rpx 0","lineHeight":"1.5","fontSize":"30rpx","color":"#333"}' class="text-gray text-content text-df">
							<rich-text :nodes="item.content"></rich-text>
						</view>
						<view :style='{"width":"100%","margin":"16rpx 0 0 0","alignItems":"center","justifyContent":"flex-end","display":"flex","height":"60rpx"}'>
							<view v-if="!comzanChange(item)&&!comcaiChange(item)" :style='{"alignItems":"center","margin":"0 20rpx 0 0","display":"flex"}' @click="comzanClick(item)">
								<span class="icon iconfont icon-zan19" :style='{"fontSize":"28rpx"}'></span>
								<span :style='{"fontSize":"28rpx","display":"none"}'>赞</span>
								<span :style='{"fontSize":"28rpx"}'>({{item.thumbsupnum}})</span>
							</view>
							<view v-if="comzanChange(item)" :style='{"margin":"0 20rpx 0 0","background":"none"}' @click="comzanClick(item)">
								<span class="icon iconfont icon-zan19" :style='{"color":"#ccaafa","fontSize":"28rpx"}'></span>
								<span :style='{"color":"#ccaafa","fontSize":"28rpx","display":"none"}'>已赞</span>
								<span :style='{"color":"#ccaafa","fontSize":"28rpx"}'>({{item.thumbsupnum}})</span>
							</view>
							<view v-if="!comzanChange(item)&&!comcaiChange(item)" :style='{"alignItems":"center","display":"flex"}' @click="comcaiClick(item)">
								<span class="icon iconfont icon-cai01" :style='{"fontSize":"28rpx"}'></span>
								<span :style='{"fontSize":"28rpx","display":"none"}'>踩</span>
								<span :style='{"fontSize":"28rpx"}'>({{item.crazilynum}})</span>
							</view>
							<view v-if="comcaiChange(item)" :style='{"background":"none"}' @click="comcaiClick(item)">
								<span class="icon iconfont icon-cai01" :style='{"color":"#ccaafa","fontSize":"28rpx"}'></span>
								<span :style='{"color":"#ccaafa","fontSize":"28rpx","display":"none"}'>已踩</span>
								<span :style='{"color":"#ccaafa","fontSize":"28rpx"}'>({{item.crazilynum}})</span>
							</view>
						</view>
						<view :style='{"color":"#999","top":"40rpx","textAlign":"left","width":"auto","lineHeight":"48rpx","fontSize":"28rpx","position":"absolute","right":"80rpx"}' class="margin-top-sm text-gray text-df">{{item.addtime}}</view>
						<view v-if="item.reply" :style='{"margin":"8rpx 0","lineHeight":"1.5","fontSize":"30rpx","color":"#333"}' class="text-gray text-content text-df">
							回复:<rich-text :nodes="item.reply"></rich-text>
						</view>
						<view style="display: flex;display: flex;justify-content: flex-end;padding: 6rpx 0;" v-if="user&&user.id==item.userid">
							<view style="color: #999;font-size: 16rpx;" @click="delClick(item.id)">删除</view>
						</view>
					</view>
				</view>

				<view class="bottom-content bg-white tabbar border shop" :style='{"padding":"48rpx 24rpx","margin":"0px auto","flexWrap":"wrap","background":"#fff","display":"flex","width":"100%","height":"auto","order":"20"}'>

					<button :style='{"border":"0","padding":"0 20rpx","boxShadow":"none","margin":"0 10rpx 10rpx 0","color":"#fff","borderRadius":"8rpx","background":"#e5b3b3","width":"auto","fontSize":"28rpx","lineHeight":"80rpx","height":"80rpx"}' v-if="userid&&isAuth('news','私聊')" @tap="chatClick">联系TA</button>
					<button :style='{"border":"0","padding":"0 20rpx","boxShadow":"none","margin":"0 10rpx 10rpx 0","color":"#fff","borderRadius":"8rpx","background":"#e5b3b3","width":"auto","fontSize":"28rpx","lineHeight":"80rpx","height":"80rpx"}' v-if="!userid&&isAuthFront('news','私聊')" @tap="chatClick">联系TA</button>
					
				</view>
			</view>
		</view>
	</view>
</mescroll-uni>
</view>
</template>

<script>
	export default {
		data() {
			return {
				btnColor: ['#409eff','#67c23a','#909399','#e6a23c','#f56c6c','#356c6c','#351c6c','#f093a9','#a7c23a','#104eff','#10441f','#a21233','#503319'],
				id: '',
				userid: '',
				detail: {},
				swiperList: [],
				commentList: [],
				mescroll: null, //mescroll实例对象
				downOption: {
					auto: false //是否在初始化后,自动执行下拉回调callback; 默认true
				},
				upOption: {
					noMoreSize: 3, //如果列表已无数据,可设置列表的总数量要大于半页才显示无更多数据;避免列表数据过少(比如只有一条数据),显示无更多数据会不好看; 默认5
					textNoMore: '~ 没有更多了 ~',
				},
				hasNext: true,
				user: {},
				storeupFlag: 0,
				thumbsupFlag: 0,
				crazilyFlag: 0,
				count: 0,
				timer: null,
				title:'',
			}
		},
		components: {
		},
		computed: {
			baseUrl() {
				return this.$base.url;
			},
		},
		async onLoad(options) {
			// #ifdef APP-PLUS
			let page = getCurrentPages()
			this.href = this.baseUrl + 'front/h5/#/' + page[page.length - 1].route
			// #endif
			let table = uni.getStorageSync("nowTable");
			// 获取用户信息
			let res = await this.$api.session(table);
			this.user = res.data;
			this.id = options.id;
			if(options.userid) {
				this.userid = options.userid;
			}
			// 渲染数据
			this.init();
			this.hasNext = true
			// 重新加载数据
			if (this.mescroll) this.mescroll.resetUpScroll()
		},
		// #ifdef MP-WEIXIN
		onShareAppMessage(){
			var obj = {
				title: this.title,
				imageUrl: this.swiperList[0]?this.baseUrl + this.swiperList[0]: ''
			}
			return obj
		},
		// #endif
		onUnload() {
			if(this.timer) {
				clearInterval(this.timer);
			}
		},
		async onShow(options) {
			let table = uni.getStorageSync("nowTable");
			// 获取用户信息
			let res = await this.$api.session(table);
			this.user = res.data;
			this.btnColor = this.btnColor.sort(()=> {
				return (0.5-Math.random());
			});
			this.getStoreup();
			this.getThumbsup();
			let cleanType = uni.getStorageSync('discussnewsCleanType')
			if(cleanType){
				uni.removeStorageSync('discussnewsCleanType')
				this.mescroll.num = 1
				this.upCallback(this.mescroll)
				this.init(2);
			}
			let crossCleanType = uni.getStorageSync('crossCleanType')
			if(crossCleanType) {
				uni.removeStorageSync('crossCleanType')
				res = await this.$api.info('news', this.id);
				let reg=new RegExp('http://localhost:8080/springbootsp85lx42/upload','g')//g代表全部
				if(res.data.content){
					res.data.content = res.data.content.replace(reg, this.$base.url + 'upload');
				}
				this.detail = res.data;
			}
		},
		destroyed: function() {
			//window.clearInterval(this.inter);
		},
		methods: {
			imgView(url){
				let arr = []
				for(let x in this.swiperList){
					arr.push(this.swiperList[x].substr(0,4)=='http'?this.swiperList[x]:this.baseUrl + this.swiperList[x])
				}
				uni.previewImage({
					current: url,
					urls: arr
				})
			},
			// 拨打电话
			callClick(row){
				uni.makePhoneCall({
					phoneNumber: row
				})
			},
			// 支付
			onPayTap(){
				let that = this
				if(!this.user){
					this.$utils.msg("请先登录")
					setTimeout(()=>{
						that.$utils.jump('../login/login')
					},1500)
					return false
				}
				uni.setStorageSync('paytable','news');
				uni.setStorageSync('payObject',this.detail);
				this.$utils.jump('../pay-confirm/pay-confirm?type=1')
			},
			onDetailTap(item) {
				uni.setStorageSync("useridTag",this.userid);
				this.$utils.jump(`./detail?id=${item.id}&userid=`+this.userid)
			},
			// 收藏
			async getStoreup() {
				if(!this.user){
					return false
				}
				let params = {
					page: 1,
					limit: 1,
					refid : this.id,
					tablename : 'news',
					userid: this.user.id,
					type: '1',
				}
				let res = await this.$api.list(`storeup`, params);
				this.storeupFlag = res.data.list.length;
			},
			async shoucang(){
				let that = this
				if(!this.user){
					this.$utils.msg("请先登录")
					setTimeout(()=>{
						that.$utils.jump('../login/login')
					},1500)
					return false
				}
				let _this = this;
				let params = {
					page: 1,
					limit: 1,
					refid : _this.detail.id,
					tablename : 'news',
					userid: _this.user.id,
					type: '1',
				}
				let res = await _this.$api.list(`storeup`, params);
				if (res.data.list.length == 1) {
					let storeupId = res.data.list[0].id;
					uni.showModal({
						title: '提示',
						content: '是否取消',
						success: async function(res) {
							if (res.confirm) {
								_this.detail.storeupnum--
								await _this.$api.update('news',_this.detail)
								await _this.$api.del('storeup', JSON.stringify([storeupId]));
								_this.$utils.msg('取消成功');
								_this.getStoreup();
							}
						}
					});
					return;
				}
				uni.showModal({
					title: '提示',
					content: '是否收藏',
					success: async function(res) {
						if (res.confirm) {
							await _this.$api.add('storeup', {
								userid: _this.user.id,
								inteltype: _this.detail.typename,
								picture: _this.swiperList[0],
								refid: _this.detail.id,
								tablename: 'news',
								type: '1'
							});
							_this.detail.storeupnum++
							await _this.$api.update('news',_this.detail)
							_this.$utils.msg('收藏成功');
							_this.getStoreup();
						}
					}
				});
			},
			// 跨表
			async onAcrossTap(tableName,crossOptAudit,crossOptPay,statusColumnName,tips,statusColumnValue,type=1){
				let that = this
				if(!this.user){
					this.$utils.msg("请先登录")
					setTimeout(()=>{
						that.$utils.jump('../login/login')
					},1500)
					return false
				}
				uni.setStorageSync('crossTable','news');
				uni.setStorageSync(`crossObj`, this.detail);
				uni.setStorageSync(`statusColumnName`, statusColumnName);
				uni.setStorageSync(`statusColumnValue`, statusColumnValue);
				uni.setStorageSync(`tips`, tips);
				if(statusColumnName!=''&&!statusColumnName.startsWith("[")) {
					var obj = uni.getStorageSync('crossObj');
					for (var o in obj){
						if(o==statusColumnName && obj[o]==statusColumnValue){
							this.$utils.msg(tips);
							return
						}
					}
				}
				this.$utils.jump(`../${tableName}/add-or-update?cross=true`);
			},
			// 获取详情
			async init(type=1){
				if(this.timer) {
					clearInterval(this.timer);
				}
				let res = await this.$api.info('news', this.id);
				let reg=new RegExp('http://localhost:8080/springbootsp85lx42/upload','g')//g代表全部
				res.data.content = res.data.content.replace(reg, this.$base.url + 'upload');
				this.detail = res.data;













				//修改富文本的图片样式
				this.detail.content = this.detail.content.replace(/img src/gi,"img style=\"width:100%;\" src");
				if(type==2){
					this.detail.discussnum++
					await this.$api.update('news',this.detail)
				}
			},
			// mescroll组件初始化的回调,可获取到mescroll对象
			mescrollInit(mescroll) {
				this.mescroll = mescroll;
			},

			/*下拉刷新的回调 */
			downCallback(mescroll) {
				this.hasNext = true
				mescroll.resetUpScroll()
			},

			/*上拉加载的回调: mescroll携带page的参数, 其中num:当前页 从1开始, size:每页数据条数,默认10 */
			async upCallback(mescroll) {
				if(uni.getStorageSync("appUserid")){
					let res = await this.$api.list('discussnews', {
						page: mescroll.num,
						limit: 10,
						refid: Number(this.id)
					});
					// 如果是第一页数据置空
					if (mescroll.num == 1) this.commentList = [];
					for(let x in res.data.list){
						if(res.data.list[x].content){
							res.data.list[x].content = res.data.list[x].content.replace(/img src/gi,"img style=\"width:100%;\" src")
						}
					}
					this.commentList = this.commentList.concat(res.data.list);
					if (res.data.list.length == 0) this.hasNext = false;
				}
				mescroll.endSuccess(mescroll.size, this.hasNext);

			},
			comzanChange(row){
				if(row.tuserids){
					let arr = String(row.tuserids).split(',')
					for(let x in arr){
						if(arr[x] == this.user.id){
							return true
						}
					}
				}
				return false
			},
			async comzanClick(row){
				if(!this.user){
					return false
				}
				if(!this.comzanChange(row)){
					row.thumbsupnum++
					if(row.tuserids){
						row.tuserids = row.tuserids + ',' + this.user.id
					}else {
						row.tuserids = this.user.id
					}
					await this.$api.update('discussnews',row)
					this.$utils.msg('点赞成功');
				}else {
					row.thumbsupnum--
					let arr = String(row.tuserids).split(',')
					for(let x in arr){
						if(arr[x] == this.user.id){
							arr.splice(x,1)
						}
					}
					row.tuserids = arr.join(',')
					await this.$api.update('discussnews',row)
					this.$utils.msg('取消成功');
				}
				this.$forceUpdate()
			},
			comcaiChange(row){
				if(row.cuserids){
					let arr = String(row.cuserids).split(',')
					for(let x in arr){
						if(arr[x] == this.user.id){
							return true
						}
					}
				}
				return false
			},
			async comcaiClick(row){
				if(!this.user){
					return false
				}
				if(!this.comcaiChange(row)){
					row.crazilynum++
					if(row.cuserids){
						row.cuserids = row.cuserids + ',' + this.user.id
					}else {
						row.cuserids = this.user.id
					}
					await this.$api.update('discussnews',row)
					this.$utils.msg('点踩成功');
				}else {
					row.crazilynum--
					let arr = String(row.cuserids).split(',')
					for(let x in arr){
						if(arr[x] == this.user.id){
							arr.splice(x,1)
						}
					}
					row.cuserids = arr.join(',')
					await this.$api.update('discussnews',row)
					this.$utils.msg('取消成功');
				}
				this.$forceUpdate()
			},



			onChatTap() {
				this.$utils.jump('../chat/chat')
			},
			// 下载
			download(url ){
				if(!url){
					return false
				}
				let _this = this;
				url=_this.$base.url +  url;
				uni.downloadFile({
					url: url,
					success: (res) => {
						if (res.statusCode === 200) {
							_this.$utils.msg('下载成功');
							// #ifdef H5
							 window.open(url);
							// #endif
							// #ifndef H5
							uni.saveFile({
								tempFilePath: res.tempFilePath, //临时路径
								success: function(obj) {
									uni.showToast({
										icon: 'success',
										mask: true,
										title: '下载成功' , 
										duration: 2000,
									});
									setTimeout(() => {
										console.log('obj.savedFilePath',obj.savedFilePath);
										var filePath = obj.savedFilePath;
										uni.openDocument({ //新开页面打开文档，支持格式：doc, xls, ppt, pdf, docx, xlsx, pptx。
											filePath: filePath,
											showMenu: true,
											success: function(res) {
												console.log('打开文档成功');
											}
										});
									}, 2000)
								}
							});
							// #endif
						}
					}
				});
			},
			//
			onCartTabTap() {
				this.$utils.tab('../shop-cart/shop-cart')
			},
			// 添加评论
			async onCommentTap() {
				let that = this
				if(!this.user){
					this.$utils.msg("请先登录")
					setTimeout(()=>{
						that.$utils.jump('../login/login')
					},1500)
					return false
				}
				let res = {}
				this.$utils.jump(`../discussnews/add-or-update?refid=${this.id}` )
			},
			delClick(id){
				let that = this
				uni.showModal({
					title: '提示',
					content: '是否删除此评论？',
					async success(res) {
						if(res.confirm){
							await that.$api.del('discussnews',JSON.stringify([id]))
							that.$utils.msg('删除成功')
							that.detail.discussnum--
							await that.$api.update('news',that.detail)
							setTimeout(()=>{
								that.upCallback(that.mescroll)
							},1500)
						}
					}
				})
			},
			// 获取赞踩
			async getThumbsup() {
				if(!this.user){
					return false
				}
				let params = {
					page: 1,
					limit: 1,
					refid: this.id,
					tablename: 'news',
					userid: this.user.id,
					type: '%2%',
				}
				let res = await this.$api.list(`storeup`, params);
				if (res.data.list.length > 0) {
					if(res.data.list[0].type=='21') {
						this.thumbsupFlag = 1;
					} else {
						this.crazilyFlag = 1;
					}
				}

			},
			// 点赞
			async zan() {
				let that = this
				if(!this.user){
					this.$utils.msg("请先登录")
					setTimeout(()=>{
						that.$utils.jump('../login/login')
					},1500)
					return false
				}
				let _this = this;
				let params = {
					page: 1,
					limit: 1,
					refid: _this.detail.id,
					tablename : 'news',
					userid: _this.user.id,
					type: '%2%',
				}
				let res = await _this.$api.list(`storeup`, params);
				if (res.data.list.length > 0) {
					let storeupId = res.data.list[0].id;
					uni.showModal({
						title: '提示',
						content: '是否取消点赞',
						success: async function(res) {
							if (res.confirm) {
								await _this.$api.del('storeup', JSON.stringify([storeupId]));
								_this.detail.thumbsupnum = parseInt(_this.detail.thumbsupnum) - 1;
								await _this.$api.update('news', _this.detail);
								_this.$utils.msg('取消成功');
								_this.thumbsupFlag=0;
							}
						}
					});
					return;
				}
				uni.showModal({
					title: '提示',
					content: '是否点赞',
					success: async function(res) {
						if (res.confirm) {
							await _this.$api.add('storeup', {
								userid: _this.user.id,
								picture: _this.swiperList[0],
								refid: _this.detail.id,
								tablename: 'news',
								type: '21'
							});
							_this.detail.thumbsupnum = parseInt(_this.detail.thumbsupnum) + 1;
							await _this.$api.update('news', _this.detail);
							_this.$utils.msg('点赞成功');
							_this.thumbsupFlag=1;
						}
					}
				});
			},
			// 踩
			async cai() {
				let that = this
				if(!this.user){
					this.$utils.msg("请先登录")
					setTimeout(()=>{
						that.$utils.jump('../login/login')
					},1500)
					return false
				}
				let _this = this;
				let params = {
					page: 1,
					limit: 1,
					refid: _this.detail.id,
					tablename: 'news',
					userid: _this.user.id,
					type: '%2%',
				}
				let res = await _this.$api.list(`storeup`, params);
				if (res.data.list.length > 0) {
					let storeupId = res.data.list[0].id;
					uni.showModal({
						title: '提示',
						content: '是否取消点踩',
						success: async function(res) {
							if (res.confirm) {
								await _this.$api.del('storeup', JSON.stringify([storeupId]));
								_this.detail.crazilynum = parseInt(_this.detail.crazilynum) - 1;
								await _this.$api.update('news', _this.detail);
								_this.$utils.msg('取消成功');
								_this.crazilyFlag=0;
							}
						}
					});
					return;
				}
				uni.showModal({
					title: '提示',
					content: '是否点踩',
					success: async function(res) {
						if (res.confirm) {
							await _this.$api.add('storeup', {
								userid: _this.user.id,
								picture: _this.swiperList[0],
								refid: _this.detail.id,
								tablename: 'news',
								type: '22'
							});
							_this.detail.crazilynum = parseInt(_this.detail.crazilynum) + 1;
							await _this.$api.update('news', _this.detail);
							_this.$utils.msg('点踩成功');
							_this.crazilyFlag=1;
						}
					}
				});
			},
		}
	}
</script>

<style lang="scss">
	page {
	  --animate-duration: 1s;
	  --animate-delay: 1s;
	  --animate-repeat: 1;
	}
	
	.content {
		min-height: calc(100vh - 44px);
		box-sizing: border-box;
	}
	
	.seat-list {
		display: flex;
		align-items: center;
		flex-wrap: wrap;
		background: #FFFFFF;
		margin: 20upx;
		border-radius: 20upx;
		padding: 20upx;
		font-size: 30upx;
		.seat-item {
			width: 33.33%;
			display: flex;
			align-items: center;
			flex-direction: column;
			margin-bottom: 20upx;
	
			.seat-icon {
				width: 50upx;
				height: 50upx;
				margin-bottom: 10upx;
			}
		}
	}
	
	audio {
		display: flex;
		flex-direction: column;
	}
	
	.audio /deep/ .uni-audio-default {
		width: inherit;
	}
	

</style>
