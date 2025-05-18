
<template>
<view>
<mescroll-uni @init="mescrollInit" :up="upOption" :down="downOption" @down="downCallback" @up="upCallback">
	<view class="content">
		<view class="container" :style='{"alignContent":"flex-start","padding":"0","borderColor":"#c0c0c0","alignItems":"flex-start","flexWrap":"wrap","background":"#fff","borderWidth":"2rpx 0 0 0","display":"flex","width":"100%","borderStyle":"solid","height":"auto"}'>
			<swiper :style='{"width":"100%","margin":"10rpx auto","background":"#fff","height":"440rpx","zIndex":"0"}' class="swiper" :indicator-dots='false' :autoplay='false' :circular='false' indicator-active-color='#000000' indicator-color='rgba(0, 0, 0, .3)' :duration='500' :interval='5000' :vertical='false'>
				<swiper-item :style='{"width":"100%","background":"#fff","height":"440rpx"}' v-for="(swiper,index) in swiperList" :key="index">
					<image :style='{"width":"100%","objectFit":"contain","display":"block","height":"440rpx"}' mode="aspectFill" v-if="swiper.substring(0,4)=='http'" :src="swiper" @tap="imgView(swiper)"></image>
					<image :style='{"width":"100%","objectFit":"contain","display":"block","height":"440rpx"}' mode="aspectFill" v-else :src="baseUrl+swiper" @tap="imgView(baseUrl+swiper)"></image>
				</swiper-item>
			</swiper>
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

				<view :style='{"padding":"0 24rpx","margin":"0 auto","borderColor":"#ccc","borderRadius":"0","borderWidth":"0 0 2rpx 0","background":"#fff","display":"flex","width":"calc(100% - 48rpx)","borderStyle":"solid","justifyContent":"flex-start","height":"auto"}' class="detail-list-item title">
					<view :style='{"padding":"0 20rpx 0 0","whiteSpace":"nowrap","color":"#333","textAlign":"left","width":"auto","lineHeight":"80rpx","fontSize":"28rpx"}' class="lable">陪玩姓名：</view>
					<view :style='{"padding":"0px","margin":"0px","lineHeight":"80rpx","fontSize":"28rpx","color":"rgb(0, 0, 0)","flex":"1"}' class="text" >{{detail.peiwanxingming}}</view>
				</view>
				<view :style='{"padding":"0 24rpx","margin":"0 auto","borderColor":"#ccc","borderRadius":"0","borderWidth":"0 0 2rpx 0","background":"#fff","display":"flex","width":"calc(100% - 48rpx)","borderStyle":"solid","justifyContent":"flex-start","height":"auto"}' class="detail-list-item title">
					<view :style='{"padding":"0 20rpx 0 0","whiteSpace":"nowrap","color":"#333","textAlign":"left","width":"auto","lineHeight":"80rpx","fontSize":"28rpx"}' class="lable">工作状态：</view>
					<view :style='{"padding":"0px","margin":"0px","lineHeight":"80rpx","fontSize":"28rpx","color":"rgb(0, 0, 0)","flex":"1"}' class="text" >{{detail.gongzuozhuangtai}}</view>
				</view>
				<view :style='{"padding":"0 24rpx","margin":"0 auto","borderColor":"#ccc","borderRadius":"0","borderWidth":"0 0 2rpx 0","background":"#fff","display":"flex","width":"calc(100% - 48rpx)","borderStyle":"solid","justifyContent":"flex-start","height":"auto"}' class="detail-list-item title">
					<view :style='{"padding":"0 20rpx 0 0","whiteSpace":"nowrap","color":"#333","textAlign":"left","width":"auto","lineHeight":"80rpx","fontSize":"28rpx"}' class="lable">陪玩收费(元/小时)：</view>
					<view :style='{"padding":"0px","margin":"0px","lineHeight":"80rpx","fontSize":"28rpx","color":"rgb(0, 0, 0)","flex":"1"}' class="text" >{{detail.peiwanshoufei}}</view>
				</view>

				<view class="detail-list-item" :style='{"padding":"0 24rpx","margin":"0 auto","borderColor":"#ccc","borderRadius":"0","borderWidth":"0 0 2rpx 0","background":"#fff","display":"flex","width":"calc(100% - 48rpx)","borderStyle":"solid","justifyContent":"flex-start","height":"auto"}'>
					<view class="lable" :style='{"padding":"0 20rpx 0 0","whiteSpace":"nowrap","color":"#333","textAlign":"left","width":"auto","lineHeight":"80rpx","fontSize":"28rpx"}'>陪玩账号：</view>
					<view class="text" :style='{"padding":"0px","margin":"0px","lineHeight":"80rpx","fontSize":"28rpx","color":"rgb(0, 0, 0)","flex":"1"}' >{{detail.peiwanzhanghao}}</view>
				</view>
				<view class="detail-list-item" :style='{"padding":"0 24rpx","margin":"0 auto","borderColor":"#ccc","borderRadius":"0","borderWidth":"0 0 2rpx 0","background":"#fff","display":"flex","width":"calc(100% - 48rpx)","borderStyle":"solid","justifyContent":"flex-start","height":"auto"}'>
					<view class="lable" :style='{"padding":"0 20rpx 0 0","whiteSpace":"nowrap","color":"#333","textAlign":"left","width":"auto","lineHeight":"80rpx","fontSize":"28rpx"}'>性别：</view>
					<view class="text" :style='{"padding":"0px","margin":"0px","lineHeight":"80rpx","fontSize":"28rpx","color":"rgb(0, 0, 0)","flex":"1"}' >{{detail.xingbie}}</view>
				</view>
				<view class="detail-list-item" :style='{"padding":"0 24rpx","margin":"0 auto","borderColor":"#ccc","borderRadius":"0","borderWidth":"0 0 2rpx 0","background":"#fff","display":"flex","width":"calc(100% - 48rpx)","borderStyle":"solid","justifyContent":"flex-start","height":"auto"}'>
					<view class="lable" :style='{"padding":"0 20rpx 0 0","whiteSpace":"nowrap","color":"#333","textAlign":"left","width":"auto","lineHeight":"80rpx","fontSize":"28rpx"}'>年龄：</view>
					<view class="text" :style='{"padding":"0px","margin":"0px","lineHeight":"80rpx","fontSize":"28rpx","color":"rgb(0, 0, 0)","flex":"1"}' >{{detail.nianling}}</view>
				</view>
				<view class="detail-list-item" :style='{"padding":"0 24rpx","margin":"0 auto","borderColor":"#ccc","borderRadius":"0","borderWidth":"0 0 2rpx 0","background":"#fff","display":"flex","width":"calc(100% - 48rpx)","borderStyle":"solid","justifyContent":"flex-start","height":"auto"}'>
					<view class="lable" :style='{"padding":"0 20rpx 0 0","whiteSpace":"nowrap","color":"#333","textAlign":"left","width":"auto","lineHeight":"80rpx","fontSize":"28rpx"}'>工作时间：</view>
					<view class="text" :style='{"padding":"0px","margin":"0px","lineHeight":"80rpx","fontSize":"28rpx","color":"rgb(0, 0, 0)","flex":"1"}' >{{detail.gongzuoshijian}}</view>
				</view>
				<view class="detail-list-item" :style='{"padding":"0 24rpx","margin":"0 auto","borderColor":"#ccc","borderRadius":"0","borderWidth":"0 0 2rpx 0","background":"#fff","display":"flex","width":"calc(100% - 48rpx)","borderStyle":"solid","justifyContent":"flex-start","height":"auto"}'>
					<view class="lable" :style='{"padding":"0 20rpx 0 0","whiteSpace":"nowrap","color":"#333","textAlign":"left","width":"auto","lineHeight":"80rpx","fontSize":"28rpx"}'>联系电话：</view>
					<view class="text" :style='{"padding":"0px","margin":"0px","lineHeight":"80rpx","fontSize":"28rpx","color":"rgb(0, 0, 0)","flex":"1"}' style="text-decoration: underline" @tap="callClick(detail.lianxidianhua)" >{{detail.lianxidianhua}}</view>
				</view>
				<view class="detail-list-item" :style='{"padding":"0 24rpx","margin":"0 auto","borderColor":"#ccc","borderRadius":"0","borderWidth":"0 0 2rpx 0","background":"#fff","display":"flex","width":"calc(100% - 48rpx)","borderStyle":"solid","justifyContent":"flex-start","height":"auto"}'>
					<view class="lable" :style='{"padding":"0 20rpx 0 0","whiteSpace":"nowrap","color":"#333","textAlign":"left","width":"auto","lineHeight":"80rpx","fontSize":"28rpx"}'>擅长游戏：</view>
					<view class="text" :style='{"padding":"0px","margin":"0px","lineHeight":"80rpx","fontSize":"28rpx","color":"rgb(0, 0, 0)","flex":"1"}' >{{detail.youxileibie}}</view>
				</view>
				<view class="detail-list-item" :style='{"padding":"0 24rpx","margin":"0 auto","borderColor":"#ccc","borderRadius":"0","borderWidth":"0 0 2rpx 0","background":"#fff","display":"flex","width":"calc(100% - 48rpx)","borderStyle":"solid","justifyContent":"flex-start","height":"auto"}'>
					<view class="lable" :style='{"padding":"0 20rpx 0 0","whiteSpace":"nowrap","color":"#333","textAlign":"left","width":"auto","lineHeight":"80rpx","fontSize":"28rpx"}'>点击次数：</view>
					<view class="text" :style='{"padding":"0px","margin":"0px","lineHeight":"80rpx","fontSize":"28rpx","color":"rgb(0, 0, 0)","flex":"1"}' >{{detail.clicknum}}</view>
				</view>
				<view class="detail-list-item" :style='{"padding":"0 24rpx","margin":"0 auto","borderColor":"#ccc","borderRadius":"0","borderWidth":"0 0 2rpx 0","background":"#fff","display":"flex","width":"calc(100% - 48rpx)","borderStyle":"solid","justifyContent":"flex-start","height":"auto"}'>
					<view class="lable" :style='{"padding":"0 20rpx 0 0","whiteSpace":"nowrap","color":"#333","textAlign":"left","width":"auto","lineHeight":"80rpx","fontSize":"28rpx"}'>收藏数：</view>
					<view class="text" :style='{"padding":"0px","margin":"0px","lineHeight":"80rpx","fontSize":"28rpx","color":"rgb(0, 0, 0)","flex":"1"}' >{{detail.storeupnum}}</view>
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




				<view class="detail-list-item rich" :style='{"padding":"0 0 0 24rpx","margin":"0 auto","borderColor":"#ccc","borderRadius":"0","borderWidth":"0 0 2rpx 0","background":"#fff","display":"flex","width":"calc(100% - 48rpx)","borderStyle":"solid","height":"auto"}'>
					<view class="lable" :style='{"padding":"0 20rpx 0 0","whiteSpace":"nowrap","color":"#333","textAlign":"right","width":"auto","lineHeight":"80rpx","fontSize":"28rpx"}'>个人介绍：</view>
					<view class="rich-text" :style='{"padding":"20rpx 24rpx 24rpx 0","margin":"0","lineHeight":"48rpx"}'>
						<rich-text :nodes="detail.gerenjieshao"></rich-text>
					</view>
				</view>



				<view class="bottom-content bg-white tabbar border shop" :style='{"padding":"48rpx 24rpx","margin":"0px auto","flexWrap":"wrap","background":"#fff","display":"flex","width":"100%","height":"auto","order":"20"}'>

					<button :style='{"border":"0","padding":"0 20rpx","boxShadow":"none","margin":"0 10rpx 10rpx 0","color":"#fff","borderRadius":"8rpx","background":"#cabd8b","width":"auto","fontSize":"28rpx","lineHeight":"80rpx","height":"80rpx"}' v-if="userid&&isAuth('congyezhe','陪玩申请')" @tap="onAcrossTap('peiwandingdan','','','gongzuozhuangtai','未上线',gongzuozhuangtaiCrossSelect[0])" class="cu-btn bg-brown round shadow-blur" >陪玩申请</button>
					<button :style='{"border":"0","padding":"0 20rpx","boxShadow":"none","margin":"0 10rpx 10rpx 0","color":"#fff","borderRadius":"8rpx","background":"#cabd8b","width":"auto","fontSize":"28rpx","lineHeight":"80rpx","height":"80rpx"}' v-if="!userid&&isAuthFront('congyezhe','陪玩申请')" @tap="onAcrossTap('peiwandingdan','','','gongzuozhuangtai','未上线',gongzuozhuangtaiCrossSelect[0])" class="cu-btn bg-brown round shadow-blur" >陪玩申请</button>
					<button :style='{"border":"0","padding":"0 20rpx","boxShadow":"none","margin":"0 10rpx 10rpx 0","color":"#fff","borderRadius":"8rpx","background":"#e5b3b3","width":"auto","fontSize":"28rpx","lineHeight":"80rpx","height":"80rpx"}' v-if="userid&&isAuth('congyezhe','私聊')" @tap="chatClick">私聊</button>
					<button :style='{"border":"0","padding":"0 20rpx","boxShadow":"none","margin":"0 10rpx 10rpx 0","color":"#fff","borderRadius":"8rpx","background":"#e5b3b3","width":"auto","fontSize":"28rpx","lineHeight":"80rpx","height":"80rpx"}' v-if="!userid&&isAuthFront('congyezhe','私聊')" @tap="chatClick">私聊</button>
					
				</view>
			</view>
		</view>
	</view>
</mescroll-uni>
	<uni-popup class="popup-content" ref="chatPopup" type="bottom" :maskClick="true" @change="clearChat">
		<view class="popup-chat">
			<view class="chat-content" id="chat-content">
				<view v-bind:key="item.id" v-for="item in chatList">
					<div v-if="item.addtime" style="width: 100%;text-align: center;font-size: 10px;color: #666;">{{timeFormat(item.addtime)}}</div>
					<view v-if="item.uid==user.id" class="right-content">
						<view v-if="item.format==1" class="text-content">{{item.content}}</view>
						<img v-else :src="item.content?baseUrl + item.content:''" @click="preViewImg(baseUrl + item.content)"
							style="width: 100px;height: 100px;object-fit: cover;" />
						<img :src="mpic?baseUrl + mpic:''" alt=""
							style="width: 40px;border-radius: 50%;height: 40px;margin: 0 0 0 10px;object-fit: cover;" />
					</view>
					<view v-else class="left-content">
						<img :src="fpic?baseUrl + fpic:''" alt=""
							style="width: 40px;border-radius: 50%;height: 40px;margin: 0 10px 0 0;object-fit: cover;" />
						<view v-if="item.format==1" class="text-content">{{item.content}}</view>
						<img v-else :src="item.content?baseUrl + item.content:''" @click="preViewImg(baseUrl + item.content)"
							style="width: 100px;height: 100px;object-fit: cover;" />
					</view>
					<view class="clear-float"></view>
				</view>
			</view>
			<view style="">
				<input v-model="chatForm.content" placeholder="请输入内容" confirm-type="send" @confirm="addChat"
					style="width: calc(100% - 20px);font-size: 14px;background: #eee;margin: 0 10px 10px;padding: 0 10px;">
				</input>
				<view style="display: flex;justify-content: space-around;">
					<button @click="addChat" style="width: auto;padding: 0 10px;background: #29A19C;font-size: 14px;border: none;color: #fff;">发送</button>
					<button @click="uploadSuccess" style="width: auto;padding: 0 10px;background: #0BB2C7;font-size: 14px;border: none;color: #fff;">上传图片</button>
				</view>
				
			</view>
		</view>
	</uni-popup>
</view>
</template>

<script>
	import timeMethod from '@/utils/timeMethod'
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
				gongzuozhuangtaiCrossSelect:'未上线,已上线'.split(','),
				count: 0,
				timer: null,
				title:'',
				chatList: [],
				chatForm: {
					content: ''
				},
				chatTimer: null,
				fpic: '',
				fname: '',
				fid: '',
				mpic: uni.getStorageSync('headportrait'),
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
			let crossCleanType = uni.getStorageSync('crossCleanType')
			if(crossCleanType) {
				uni.removeStorageSync('crossCleanType')
				res = await this.$api.info('congyezhe', this.id);
				let reg=new RegExp('http://localhost:8080/springbootsp85lx42/upload','g')//g代表全部
				if(res.data.gerenjieshao){
					res.data.gerenjieshao = res.data.gerenjieshao.replace(reg, this.$base.url + 'upload');
				}
				this.detail = res.data;
				this.title = this.detail.peiwanxingming
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
				uni.setStorageSync('paytable','congyezhe');
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
					tablename : 'congyezhe',
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
					tablename : 'congyezhe',
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
								await _this.$api.update('congyezhe',_this.detail)
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
								name: _this.detail.peiwanxingming,
								picture: _this.swiperList[0],
								refid: _this.detail.id,
								tablename: 'congyezhe',
								type: '1'
							});
							_this.detail.storeupnum++
							await _this.$api.update('congyezhe',_this.detail)
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
				uni.setStorageSync('crossTable','congyezhe');
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
				let res = await this.$api.info('congyezhe', this.id);
				if (res.data.touxiang) {
					this.fpic = res.data.touxiang.split(',')[0]
				} else if (res.data.headportrait) {
					this.fpic = res.data.headportrait.split(',')[0]
				}
				if(res.data.peiwanzhanghao){
					this.fname = res.data.peiwanzhanghao
				}
				this.fid = res.data.id
				let reg=new RegExp('http://localhost:8080/springbootsp85lx42/upload','g')//g代表全部
				res.data.gerenjieshao = res.data.gerenjieshao.replace(reg, this.$base.url + 'upload');
				this.detail = res.data;

				this.title = this.detail.peiwanxingming



				// 轮播图片
				this.swiperList = this.detail.touxiang ? this.detail.touxiang.split(",") : [];
				









				//修改富文本的图片样式
				this.detail.gerenjieshao = this.detail.gerenjieshao.replace(/img src/gi,"img style=\"width:100%;\" src");











				if(type==2){
					this.detail.discussnum++
					await this.$api.update('congyezhe',this.detail)
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
				mescroll.endSuccess(mescroll.size, this.hasNext);

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
			// 获取赞踩
			async getThumbsup() {
				if(!this.user){
					return false
				}
				let params = {
					page: 1,
					limit: 1,
					refid: this.id,
					tablename: 'congyezhe',
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
					tablename : 'congyezhe',
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
								await _this.$api.update('congyezhe', _this.detail);
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
								name: _this.detail.peiwanxingming,
								picture: _this.swiperList[0],
								refid: _this.detail.id,
								tablename: 'congyezhe',
								type: '21'
							});
							_this.detail.thumbsupnum = parseInt(_this.detail.thumbsupnum) + 1;
							await _this.$api.update('congyezhe', _this.detail);
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
					tablename: 'congyezhe',
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
								await _this.$api.update('congyezhe', _this.detail);
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
								name: _this.detail.peiwanxingming,
								picture: _this.swiperList[0],
								refid: _this.detail.id,
								tablename: 'congyezhe',
								type: '22'
							});
							_this.detail.crazilynum = parseInt(_this.detail.crazilynum) + 1;
							await _this.$api.update('congyezhe', _this.detail);
							_this.$utils.msg('点踩成功');
							_this.crazilyFlag=1;
						}
					}
				});
			},
			chatClick() {
				let that = this
				if(!this.user){
					this.$utils.msg("请先登录")
					setTimeout(()=>{
						that.$utils.jump('../login/login')
					},1500)
					return false
				}
				if(this.detail.id==this.user.id){
					this.$utils.msg('不能给自己发信息！');
					return false
				}
				this.getChatList()
				this.$refs.chatPopup.open()
			},
			formatMessages(messages) {
				let lastTime = null;
				messages.forEach((message, index) => {
					const currentTime = new Date(message.addtime).getTime();
					if (lastTime !== null) {
						const timeDiff = (currentTime - lastTime) / 1000 / 60; // 转换为分钟
						if (timeDiff < 3) {
							message.addtime = ''; // 如果小于3分钟，不显示时间
						}
					}
					lastTime = currentTime;
				});
				return messages;
			},
			timeFormat(time) {
				const Time = timeMethod.getTime(time).split("T");
				//当前消息日期属于周
				const week = timeMethod.getDateToWeek(time);
				//当前日期0时
				const nti = timeMethod.setTimeZero(timeMethod.getNowTime());
				//消息日期当天0时
				const mnti = timeMethod.setTimeZero(timeMethod.getTime(time));
				//计算日期差值
				const diffDate = timeMethod.calculateTime(nti, mnti);
				//本周一日期0时 （后面+1是去除当天时间）
				const fwnti = timeMethod.setTimeZero(timeMethod.countDateStr(-timeMethod.getDateToWeek(timeMethod
					.getNowTime()).weekID + 1));
				//计算周日期差值
				const diffWeek = timeMethod.calculateTime(mnti, fwnti);
			
				if (diffDate === 0) { //消息发送日期减去当天日期如果等于0则是当天时间
					return Time[1].slice(0, 5);
				} else if (diffDate < 172800000) { //当前日期减去消息发送日期小于2天（172800000ms）则是昨天-  一天最大差值前天凌晨00:00:00到今天晚上23:59:59
					return "昨天 " + Time[1].slice(0, 5);
				} else if (diffWeek >= 0) { //消息日期减去本周一日期大于0则是本周
					return week.weekName;
				} else { //其他时间则是日期
					return Time[0].slice(5, 10);
				}
			},
			async getChatList() {
				let res = await this.$api.mlist('chatmessage',{
					page: 1,
					limit: 1000,
					uid: this.user.id,
					fid: this.fid
				})
				this.chatList = this.formatMessages(res.data.list)
				// #ifdef H5
				let div = document.getElementsByClassName('chat-content')[0]
				setTimeout(() => {
					if (div)
						div.scrollTop = div.scrollHeight
				}, 0)
				// #endif
				this.chatTimer = setTimeout(() => {
					this.getChatList()
				}, 5000)
				
			},
			clearChat(e) {
				if(!e.show){
					clearTimeout(this.chatTimer)
				}
			},
			preViewImg(img){
				uni.previewImage({
					urls: [img],
					current:img
				})
			},
			async uploadSuccess() {
				clearTimeout(this.chatTimer)
				let _this = this;
				await this.$api.upload(async function(obj) {
					let res = await _this.$api.page('friend', {
						uid: _this.user.id,
						fid: _this.fid,
					})
					if(!res.data.list.length){
						await _this.$api.add('friend',{
							uid: _this.user.id,
							fid: _this.fid,
							name: _this.fname,
							picture: _this.fpic,
							type: 2,
							tablename:  'congyezhe',
						})
						await _this.$api.add('friend',{
							fid: _this.user.id,
							uid: _this.fid,
							name: uni.getStorageSync("nickname"),
							picture: _this.mpic,
							type: 2,
							tablename: uni.getStorageSync("nowTable")
						})
					}
					await _this.$api.add('chatmessage',{
						uid: _this.user.id,
						fid: _this.fid,
						content: 'upload/' + obj.file,
						format: 2
					})
					_this.chatForm = {
						content: ''
					}
					_this.getChatList()
				})
			},
			async addChat() {
				clearTimeout(this.chatTimer)
				let res = await this.$api.page('friend', {
					uid: this.user.id,
					fid: this.fid,
				})
				if(!res.data.list.length){
					await this.$api.add('friend',{
						uid: this.user.id,
						fid: this.fid,
						name: this.fname,
						picture: this.fpic,
						type: 2,
						tablename:  'congyezhe',
					})
					await this.$api.add('friend',{
						fid: this.user.id,
						uid: this.fid,
						name: uni.getStorageSync("nickname"),
						picture: this.mpic,
						type: 2,
						tablename: uni.getStorageSync("nowTable")
					})
				}
				await this.$api.add('chatmessage',{
					uid: this.user.id,
					fid: this.fid,
					content: this.chatForm.content,
					format: 1
				})
				this.chatForm = {
					content: ''
				}
				this.getChatList()
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
	

	.popup-chat{
		 background: #fff;
		 padding-bottom: 40px;
		 .chat-content {
			padding-bottom: 20px;
			width: 100%;
			margin-bottom: 10px;
			max-height: 400px;
			height: 400px;
			overflow-y: scroll;
			border: 1px solid #eeeeee;
			background: #eee;
			display: flex;
			flex-direction: column;
			
		 
			.left-content {
				float: left;
				margin-bottom: 10px;
				padding: 10px;
				max-width: 80%;
				display: flex;
				align-items: center;
				.text-content{
					background: #e5ffff;
					padding: 8px 12px;
					border-radius: 5px;
				}
			}
					 
			.right-content {
				float: right;
				margin-bottom: 10px;
				padding: 10px;
				max-width: 80%;
				display: flex;
				align-items: center;
				.text-content{
					background: #fff;
					padding: 8px 12px;
					border-radius: 5px;
				}
			}
		 }
	}
</style>
