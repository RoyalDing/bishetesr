
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

				<view :style='{"padding":"0 24rpx","margin":"0 auto","borderColor":"#ccc","borderRadius":"0","borderWidth":"0 0 2rpx 0","background":"#fff","display":"flex","width":"calc(100% - 48rpx)","borderStyle":"solid","justifyContent":"flex-start","height":"auto"}' class="detail-list-item title">
					<view :style='{"padding":"0 20rpx 0 0","whiteSpace":"nowrap","color":"#333","textAlign":"left","width":"auto","lineHeight":"80rpx","fontSize":"28rpx"}' class="lable">陪玩姓名：</view>
					<view :style='{"padding":"0px","margin":"0px","lineHeight":"80rpx","fontSize":"28rpx","color":"rgb(0, 0, 0)","flex":"1"}' class="text" >{{detail.peiwanxingming}}</view>
				</view>
				<view :style='{"padding":"0 24rpx","margin":"0 auto","borderColor":"#ccc","borderRadius":"0","borderWidth":"0 0 2rpx 0","background":"#fff","display":"flex","width":"calc(100% - 48rpx)","borderStyle":"solid","justifyContent":"flex-start","height":"auto"}' class="detail-list-item title">
					<view :style='{"padding":"0 20rpx 0 0","whiteSpace":"nowrap","color":"#333","textAlign":"left","width":"auto","lineHeight":"80rpx","fontSize":"28rpx"}' class="lable">总费用：</view>
					<view :style='{"padding":"0px","margin":"0px","lineHeight":"80rpx","fontSize":"28rpx","color":"rgb(0, 0, 0)","flex":"1"}' class="text" >{{detail.zongfeiyong}}</view>
				</view>

				<view class="detail-list-item" :style='{"padding":"0 24rpx","margin":"0 auto","borderColor":"#ccc","borderRadius":"0","borderWidth":"0 0 2rpx 0","background":"#fff","display":"flex","width":"calc(100% - 48rpx)","borderStyle":"solid","justifyContent":"flex-start","height":"auto"}'>
					<view class="lable" :style='{"padding":"0 20rpx 0 0","whiteSpace":"nowrap","color":"#333","textAlign":"left","width":"auto","lineHeight":"80rpx","fontSize":"28rpx"}'>陪玩单号：</view>
					<view class="text" :style='{"padding":"0px","margin":"0px","lineHeight":"80rpx","fontSize":"28rpx","color":"rgb(0, 0, 0)","flex":"1"}' >{{detail.peiwandanhao}}</view>
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
					<view class="lable" :style='{"padding":"0 20rpx 0 0","whiteSpace":"nowrap","color":"#333","textAlign":"left","width":"auto","lineHeight":"80rpx","fontSize":"28rpx"}'>游戏类别：</view>
					<view class="text" :style='{"padding":"0px","margin":"0px","lineHeight":"80rpx","fontSize":"28rpx","color":"rgb(0, 0, 0)","flex":"1"}' >{{detail.youxileibie}}</view>
				</view>
				<view class="detail-list-item" :style='{"padding":"0 24rpx","margin":"0 auto","borderColor":"#ccc","borderRadius":"0","borderWidth":"0 0 2rpx 0","background":"#fff","display":"flex","width":"calc(100% - 48rpx)","borderStyle":"solid","justifyContent":"flex-start","height":"auto"}'>
					<view class="lable" :style='{"padding":"0 20rpx 0 0","whiteSpace":"nowrap","color":"#333","textAlign":"left","width":"auto","lineHeight":"80rpx","fontSize":"28rpx"}'>陪玩游戏：</view>
					<view class="text" :style='{"padding":"0px","margin":"0px","lineHeight":"80rpx","fontSize":"28rpx","color":"rgb(0, 0, 0)","flex":"1"}' >{{detail.peiwanyouxi}}</view>
				</view>
				<view class="detail-list-item" :style='{"padding":"0 24rpx","margin":"0 auto","borderColor":"#ccc","borderRadius":"0","borderWidth":"0 0 2rpx 0","background":"#fff","display":"flex","width":"calc(100% - 48rpx)","borderStyle":"solid","justifyContent":"flex-start","height":"auto"}'>
					<view class="lable" :style='{"padding":"0 20rpx 0 0","whiteSpace":"nowrap","color":"#333","textAlign":"left","width":"auto","lineHeight":"80rpx","fontSize":"28rpx"}'>陪玩收费：</view>
					<view class="text" :style='{"padding":"0px","margin":"0px","lineHeight":"80rpx","fontSize":"28rpx","color":"rgb(0, 0, 0)","flex":"1"}' >{{detail.peiwanshoufei}}</view>
				</view>
				<view class="detail-list-item" :style='{"padding":"0 24rpx","margin":"0 auto","borderColor":"#ccc","borderRadius":"0","borderWidth":"0 0 2rpx 0","background":"#fff","display":"flex","width":"calc(100% - 48rpx)","borderStyle":"solid","justifyContent":"flex-start","height":"auto"}'>
					<view class="lable" :style='{"padding":"0 20rpx 0 0","whiteSpace":"nowrap","color":"#333","textAlign":"left","width":"auto","lineHeight":"80rpx","fontSize":"28rpx"}'>陪玩时间：</view>
					<view class="text" :style='{"padding":"0px","margin":"0px","lineHeight":"80rpx","fontSize":"28rpx","color":"rgb(0, 0, 0)","flex":"1"}' >{{detail.peiwanshijian}}</view>
				</view>
				<view class="detail-list-item" :style='{"padding":"0 24rpx","margin":"0 auto","borderColor":"#ccc","borderRadius":"0","borderWidth":"0 0 2rpx 0","background":"#fff","display":"flex","width":"calc(100% - 48rpx)","borderStyle":"solid","justifyContent":"flex-start","height":"auto"}'>
					<view class="lable" :style='{"padding":"0 20rpx 0 0","whiteSpace":"nowrap","color":"#333","textAlign":"left","width":"auto","lineHeight":"80rpx","fontSize":"28rpx"}'>用户账号：</view>
					<view class="text" :style='{"padding":"0px","margin":"0px","lineHeight":"80rpx","fontSize":"28rpx","color":"rgb(0, 0, 0)","flex":"1"}' >{{detail.yonghuzhanghao}}</view>
				</view>
				<view class="detail-list-item" :style='{"padding":"0 24rpx","margin":"0 auto","borderColor":"#ccc","borderRadius":"0","borderWidth":"0 0 2rpx 0","background":"#fff","display":"flex","width":"calc(100% - 48rpx)","borderStyle":"solid","justifyContent":"flex-start","height":"auto"}'>
					<view class="lable" :style='{"padding":"0 20rpx 0 0","whiteSpace":"nowrap","color":"#333","textAlign":"left","width":"auto","lineHeight":"80rpx","fontSize":"28rpx"}'>用户姓名：</view>
					<view class="text" :style='{"padding":"0px","margin":"0px","lineHeight":"80rpx","fontSize":"28rpx","color":"rgb(0, 0, 0)","flex":"1"}' >{{detail.yonghuxingming}}</view>
				</view>
				<view class="detail-list-item" :style='{"padding":"0 24rpx","margin":"0 auto","borderColor":"#ccc","borderRadius":"0","borderWidth":"0 0 2rpx 0","background":"#fff","display":"flex","width":"calc(100% - 48rpx)","borderStyle":"solid","justifyContent":"flex-start","height":"auto"}'>
					<view class="lable" :style='{"padding":"0 20rpx 0 0","whiteSpace":"nowrap","color":"#333","textAlign":"left","width":"auto","lineHeight":"80rpx","fontSize":"28rpx"}'>联系方式：</view>
					<view class="text" :style='{"padding":"0px","margin":"0px","lineHeight":"80rpx","fontSize":"28rpx","color":"rgb(0, 0, 0)","flex":"1"}' style="text-decoration: underline" @tap="callClick(detail.lianxifangshi)" >{{detail.lianxifangshi}}</view>
				</view>
				<view class="detail-list-item" :style='{"padding":"0 24rpx","margin":"0 auto","borderColor":"#ccc","borderRadius":"0","borderWidth":"0 0 2rpx 0","background":"#fff","display":"flex","width":"calc(100% - 48rpx)","borderStyle":"solid","justifyContent":"flex-start","height":"auto"}'>
					<view class="lable" :style='{"padding":"0 20rpx 0 0","whiteSpace":"nowrap","color":"#333","textAlign":"left","width":"auto","lineHeight":"80rpx","fontSize":"28rpx"}'>下单时间：</view>
					<view class="text" :style='{"padding":"0px","margin":"0px","lineHeight":"80rpx","fontSize":"28rpx","color":"rgb(0, 0, 0)","flex":"1"}' >{{detail.xiadanshijian}}</view>
				</view>




				<view v-if="userid" class="detail-list-item" :style='{"padding":"0 24rpx","margin":"0 auto","borderColor":"#ccc","borderRadius":"0","borderWidth":"0 0 2rpx 0","background":"#fff","display":"flex","width":"calc(100% - 48rpx)","borderStyle":"solid","justifyContent":"flex-start","height":"auto"}'>
					<view class="lable" :style='{"padding":"0 20rpx 0 0","whiteSpace":"nowrap","color":"#333","textAlign":"left","width":"auto","lineHeight":"80rpx","fontSize":"28rpx"}'>审核状态：</view>
					<view v-if="detail.sfsh=='是'" class="text" :style='{"padding":"0px","margin":"0px","lineHeight":"80rpx","fontSize":"28rpx","color":"rgb(0, 0, 0)","flex":"1"}'>通过</view>
					<view v-if="detail.sfsh=='否'" class="text" :style='{"padding":"0px","margin":"0px","lineHeight":"80rpx","fontSize":"28rpx","color":"rgb(0, 0, 0)","flex":"1"}'>不通过</view>
					<view v-if="detail.sfsh=='待审核'" class="text" :style='{"padding":"0px","margin":"0px","lineHeight":"80rpx","fontSize":"28rpx","color":"rgb(0, 0, 0)","flex":"1"}'>待审核</view>
				</view>
				<view v-if="userid" class="detail-list-item" :style='{"padding":"0 24rpx","margin":"0 auto","borderColor":"#ccc","borderRadius":"0","borderWidth":"0 0 2rpx 0","background":"#fff","display":"flex","width":"calc(100% - 48rpx)","borderStyle":"solid","justifyContent":"flex-start","height":"auto"}'>
					<view class="lable" :style='{"padding":"0 20rpx 0 0","whiteSpace":"nowrap","color":"#333","textAlign":"left","width":"auto","lineHeight":"80rpx","fontSize":"28rpx"}'>审核回复</view>
					<view class="text" :style='{"padding":"0px","margin":"0px","lineHeight":"80rpx","fontSize":"28rpx","color":"rgb(0, 0, 0)","flex":"1"}'>{{detail.shhf}}</view>
				</view>




				<view class="bottom-content bg-white tabbar border shop" :style='{"padding":"48rpx 24rpx","margin":"0px auto","flexWrap":"wrap","background":"#fff","display":"flex","width":"100%","height":"auto","order":"20"}'>

					<button :style='{"border":"0","padding":"0 20rpx","boxShadow":"none","margin":"0 10rpx 10rpx 0","color":"#fff","borderRadius":"8rpx","background":"#8bcaae","width":"auto","fontSize":"28rpx","lineHeight":"80rpx","minWidth":"150rpx","height":"80rpx"}' @tap="onPayTap" v-if="userid&&isAuth('peiwandingdan','支付') && detail.ispay!='已支付'"  class="cu-btn bg-brown round shadow-blur">支付</button>
					<button :style='{"border":"0","padding":"0 20rpx","boxShadow":"none","margin":"0 10rpx 10rpx 0","color":"#fff","borderRadius":"8rpx","background":"#8bcaae","width":"auto","fontSize":"28rpx","lineHeight":"80rpx","minWidth":"150rpx","height":"80rpx"}' @tap="onPayTap" v-if="!userid&&isAuthFront('peiwandingdan','支付') && detail.ispay!='已支付'"  class="cu-btn bg-brown round shadow-blur">支付</button>
					<button :style='{"border":"0","padding":"0 20rpx","boxShadow":"none","margin":"0 10rpx 10rpx 0","color":"#fff","borderRadius":"8rpx","background":"#8bcaae","width":"auto","fontSize":"28rpx","lineHeight":"80rpx","minWidth":"150rpx","height":"80rpx"}' v-if="!isAuth('peiwandingdan','支付') && detail.ispay!='已支付'" class="cu-btn bg-brown round shadow-blur">未支付</button>
					<button :style='{"border":"0","padding":"0 20rpx","boxShadow":"none","margin":"0 10rpx 10rpx 0","color":"#fff","borderRadius":"8rpx","background":"#8bcaae","width":"auto","fontSize":"28rpx","lineHeight":"80rpx","minWidth":"150rpx","height":"80rpx"}' v-if="detail.ispay=='已支付'"  class="cu-btn bg-brown round shadow-blur">已支付</button>
					<button :style='{"border":"0","padding":"0 20rpx","boxShadow":"none","margin":"0 10rpx 10rpx 0","color":"#fff","borderRadius":"8rpx","background":"#cabd8b","width":"auto","fontSize":"28rpx","lineHeight":"80rpx","height":"80rpx"}' v-if="userid&&isAuth('peiwandingdan','陪玩评价')" @tap="onAcrossTap('peiwanpingjia','是','','[1]','已评价')" class="cu-btn bg-brown round shadow-blur" >陪玩评价</button>
					<button :style='{"border":"0","padding":"0 20rpx","boxShadow":"none","margin":"0 10rpx 10rpx 0","color":"#fff","borderRadius":"8rpx","background":"#cabd8b","width":"auto","fontSize":"28rpx","lineHeight":"80rpx","height":"80rpx"}' v-if="!userid&&isAuthFront('peiwandingdan','陪玩评价')" @tap="onAcrossTap('peiwanpingjia','是','','[1]','已评价')" class="cu-btn bg-brown round shadow-blur" >陪玩评价</button>
					<button :style='{"border":"0","padding":"0 20rpx","boxShadow":"none","margin":"0 10rpx 10rpx 0","color":"#fff","borderRadius":"8rpx","background":"#e5b3b3","width":"auto","fontSize":"28rpx","lineHeight":"80rpx","height":"80rpx"}' v-if="userid&&isAuth('peiwandingdan','审核')" @tap="onSHTap">审核</button>
					<button :style='{"border":"0","padding":"0 20rpx","boxShadow":"none","margin":"0 10rpx 10rpx 0","color":"#fff","borderRadius":"8rpx","background":"#e5b3b3","width":"auto","fontSize":"28rpx","lineHeight":"80rpx","height":"80rpx"}' v-if="!userid&&isAuthFront('peiwandingdan','审核')" @tap="onSHTap">审核</button>
					<button :style='{"border":"0","padding":"0 20rpx","boxShadow":"none","margin":"0 10rpx 10rpx 0","color":"#fff","borderRadius":"8rpx","background":"#e5b3b3","width":"auto","fontSize":"28rpx","lineHeight":"80rpx","height":"80rpx"}' v-if="userid&&isAuth('peiwandingdan','私聊')" @tap="chatClick">联系TA</button>
					<button :style='{"border":"0","padding":"0 20rpx","boxShadow":"none","margin":"0 10rpx 10rpx 0","color":"#fff","borderRadius":"8rpx","background":"#e5b3b3","width":"auto","fontSize":"28rpx","lineHeight":"80rpx","height":"80rpx"}' v-if="!userid&&isAuthFront('peiwandingdan','私聊')" @tap="chatClick">联系TA</button>
					
				</view>
			</view>
		</view>
		<!-- 确认完成弹窗 -->
		<uni-popup class="popup-content" ref="popup" type="center">
			<form class="popup-form" style="background: #fff;width: 300px;display: block;border-radius: 10px;padding: 20px;text-align: center;">
				<view class=" margin-top">
					<picker @change="sfshChange" :value="sfshIndex" :range="sfshOptions">
						<view class="uni-input">{{detail.sfsh?detail.sfsh:'选择审核结果'}}</view>
					</picker>
				</view>
				<view class="">
					<!-- <view class="title">审核回复</view> -->
					<textarea style="width: 200px;" v-model="detail.shhf" placeholder="审核回复"></textarea>
					<!-- <input v-model="douyinId" placeholder="审核回复" name="input"></input> -->
				</view>
				<view class="btn-content">
					<button style="margin: 0 10px" @tap="onCloseWinTap" class="cu-btn bg-cyan">取消</button>
					<button style="margin: 0 10px" @tap="onFinishTap" class="cu-btn bg-red">确认</button>
				</view>
			</form>
		</uni-popup>
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
				sfshIndex: -1,
				sfshOptions: ['通过','不通过', '待审核'],
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
			let crossCleanType = uni.getStorageSync('crossCleanType')
			if(crossCleanType) {
				uni.removeStorageSync('crossCleanType')
				res = await this.$api.info('peiwandingdan', this.id);
				let reg=new RegExp('http://localhost:8080/springbootsp85lx42/upload','g')//g代表全部
				this.detail = res.data;
				this.title = this.detail.peiwanxingming
			}
			let payType = uni.getStorageSync('payType')
			if(payType){
				uni.removeStorageSync('payType')
				this.mescroll.num = 1
				this.upCallback(this.mescroll)
				this.init();
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
				if(this.detail.sfsh!='是') {
					this.$utils.msg("请审核通过后再操作");
					return
				}
				uni.setStorageSync('paytable','peiwandingdan');
				uni.setStorageSync('payObject',this.detail);
				this.$utils.jump('../pay-confirm/pay-confirm?type=1')
			},
			onDetailTap(item) {
				uni.setStorageSync("useridTag",this.userid);
				this.$utils.jump(`./detail?id=${item.id}&userid=`+this.userid)
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
				if(crossOptAudit=='是'&&this.detail.sfsh!='是') {
					this.$utils.msg("请审核通过后再操作");
					return
				}
				if(crossOptPay=='是'&&this.detail.ispay!='已支付') {
					this.$utils.msg('请支付完成再操作')
					return
				}
				uni.setStorageSync('crossTable','peiwandingdan');
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
				let res = await this.$api.info('peiwandingdan', this.id);
				let reg=new RegExp('http://localhost:8080/springbootsp85lx42/upload','g')//g代表全部
				this.detail = res.data;

				this.title = this.detail.peiwanxingming



				// 轮播图片
				this.swiperList = this.detail.touxiang ? this.detail.touxiang.split(",") : [];
				














				if(type==2){
					this.detail.discussnum++
					await this.$api.update('peiwandingdan',this.detail)
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
			onSHTap() {
				if(this.detail.sfsh=='是'||this.detail.sfsh=='否') {
					this.$utils.msg('已审核完成');
					return;
				}
				this.$refs.popup.open()
			},
			// 完成审核
			async onFinishTap() {
				if(!this.detail.sfsh){
					this.$utils.msg('请选择审核状态');
					return
				}
				if(!this.detail.shhf){
					this.$utils.msg('请填写审核回复');
					return
				}
				if(this.detail.sfsh=="通过"){
					this.detail.sfsh = '是'
				}
				if(this.detail.sfsh=="不通过"){
					this.detail.sfsh = '否'
				}
				if(this.detail.sfsh=="待审核"){
					this.detail.sfsh = '待审核'
				}
				await this.$api.update('peiwandingdan', this.detail);
				this.$utils.msg('审核成功');
				this.$refs.popup.close();
			},
			// 关闭窗口
			onCloseWinTap() {
				this.$refs.popup.close()
			},
			sfshChange(e){
				this.sfshIndex = e.target.value
				this.detail.sfsh = this.sfshOptions[this.sfshIndex]
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
