<template>
	<view class="content">
		<view :style='{"alignContent":"flex-start","padding":"0","borderColor":"#c0c0c0","alignItems":"flex-start","flexWrap":"wrap","background":"url(http://codegen.caihongy.cn/20241125/78c8aec4171c462aae36190d2433ba44.jpg) no-repeat center top / 100% auto,#fff","borderWidth":"2rpx 0 0 0","display":"flex","width":"100%","borderStyle":"solid","height":"auto"}'>
			<view v-if="user&&user.id" :style='{"minHeight":"360rpx","padding":"48rpx 24rpx 0","margin":"0","borderRadius":"0","background":"none","display":"flex","width":"100%","position":"relative","height":"auto"}' @tap="onPageTap('../user-info/user-info')" class="header" v-bind:class="{'status':isH5Plus}">
				<view :style='{"width":"100%","position":"relative","flexWrap":"wrap","flexDirection":"row","display":"flex","height":"auto"}' v-if="tableName=='yonghu'" class="userinfo">
					<image :style='{"width":"136rpx","padding":"0","margin":"0 20rpx","borderRadius":"8rpx","float":"left","height":"136rpx"}' :src="user.touxiang?baseUrl+user.touxiang:require('../../static/gen/upload.png')"></image>
					<view :style='{"width":"calc(100% - 180rpx)","flexDirection":"column","background":"none","justifyContent":"center","display":"flex"}' class="info">
						<view :style='{"width":"100%","padding":"0 40rpx 0 0","lineHeight":"48rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}'>{{user.yonghuzhanghao}}<text v-if="user.vip&& user.vip=='是'">(VIP)</text></view>
					</view>
					
					<view :style='{"padding":"20rpx","margin":"48rpx 0 0","color":"#333","borderRadius":"20rpx","flexWrap":"wrap","background":"linear-gradient(30deg, rgba(242,239,219,1) 0%, rgba(170,210,255,1) 100%)","display":"flex","width":"100%","clear":"both","fontSize":"28rpx","order":"5"}' class="info">
						<view :style='{"padding":"0 20rpx","margin":"0 3% 0 0","borderRadius":"20rpx","flexDirection":"column","background":"rgba(255,255,255,.5)","display":"flex","width":"32%","lineHeight":"48rpx","fontSize":"inherit","order":"-1"}'>
							<span :style='{"color":"inherit","whiteSpace":"nowrap"}'>联系方式：</span>
							<span :style='{"color":"inherit"}'>{{user.lianxifangshi}}</span>
						</view>
					</view>
				</view>
				<view :style='{"width":"100%","position":"relative","flexWrap":"wrap","flexDirection":"row","display":"flex","height":"auto"}' v-if="tableName=='congyezhe'" class="userinfo">
					<image :style='{"width":"136rpx","padding":"0","margin":"0 20rpx","borderRadius":"8rpx","float":"left","height":"136rpx"}' :src="user.touxiang?baseUrl+user.touxiang:require('../../static/gen/upload.png')"></image>
					<view :style='{"width":"calc(100% - 180rpx)","flexDirection":"column","background":"none","justifyContent":"center","display":"flex"}' class="info">
						<view :style='{"width":"100%","padding":"0 40rpx 0 0","lineHeight":"48rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}'>{{user.peiwanzhanghao}}<text v-if="user.vip&& user.vip=='是'">(VIP)</text></view>
					</view>
					
					<view :style='{"padding":"20rpx","margin":"48rpx 0 0","color":"#333","borderRadius":"20rpx","flexWrap":"wrap","background":"linear-gradient(30deg, rgba(242,239,219,1) 0%, rgba(170,210,255,1) 100%)","display":"flex","width":"100%","clear":"both","fontSize":"28rpx","order":"5"}' class="info">
						<view :style='{"padding":"0 20rpx","margin":"0 3% 0 0","borderRadius":"20rpx","flexDirection":"column","background":"rgba(255,255,255,.5)","display":"flex","width":"32%","lineHeight":"48rpx","fontSize":"inherit","order":"-1"}'>
							<span :style='{"color":"inherit","whiteSpace":"nowrap"}'>联系电话：</span>
							<span :style='{"color":"inherit"}'>{{user.lianxidianhua}}</span>
						</view>
					</view>
					<view :style='{"border":"0px solid #ffffff80","padding":"0px","margin":"30rpx 0","borderRadius":"20rpx","background":"rgba(255,255,255,0)","display":"flex","width":"calc(100% + 0px) ","order":"10"}'>
					  <view :style='{"border":"0px solid #9a9a9a","padding":"10rpx","margin":"0 0px 0 0","borderRadius":"12rpx","background":"#b0cb5e","display":"flex","width":"100%","justifyContent":"center"}'>
					    <text class="icon iconfont icon-zan10" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"28rpx","color":"#fff","order":"2"}'></text>
					    <text :style='{"margin":"0 20rpx 0 0","lineHeight":"1.5","fontSize":"28rpx","color":"#fff"}'>点赞 {{user.thumbsnum}}</text>
					  </view>
					  <view :style='{"border":"0px solid #9a9a9a","padding":"10rpx","margin":"0 0px 0 0","borderRadius":"12rpx","background":"#8fb9e9","display":"flex","width":"100%","justifyContent":"center"}'>
					    <text class="icon iconfont icon-shoucang10" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"28rpx","color":"#fff","order":"2"}'></text>
					    <text :style='{"margin":"0 20rpx 0 0","lineHeight":"1.5","fontSize":"28rpx","color":"#fff"}'>收藏 {{user.storenum}}</text>
					  </view>
					</view>
				</view>
				<view :style='{"padding":"4rpx 20rpx 4rpx 10rpx","alignItems":"center","borderRadius":"40rpx 0 0 40rpx","top":"40rpx","background":"#b0cb5e","flexDirection":"row","display":"flex","width":"160rpx","position":"absolute","right":"0","justifyContent":"center","height":"auto"}' class="setting">
					<text class="icon iconfont icon-qita6" :style='{"border":"0","margin":"0 10rpx 0 0","color":"#fff","borderRadius":"0","width":"40rpx","lineHeight":"40rpx","fontSize":"44rpx"}'></text>
					<text :style='{"color":"#fff","lineHeight":"60rpx","fontSize":"28rpx"}'>设置</text>
				</view>
			</view>
			
			<view v-else :style='{"minHeight":"360rpx","padding":"48rpx 24rpx 0","margin":"0","borderRadius":"0","background":"none","display":"flex","width":"100%","position":"relative","height":"auto"}' @tap="loginClick" class="header" v-bind:class="{'status':isH5Plus}">
				<view :style='{"alignItems":"center","color":"#333","background":"none","display":"flex","width":"100%","fontSize":"36rpx","justifyContent":"center","height":"200rpx"}'>登录/注册</view>
			</view>
			
			<view :style='{"width":"100%","background":"none","height":"auto"}' class="list">
				
				<view :style='{"width":"calc(100% - 48rpx)","padding":"0px 0 0","margin":"40rpx auto","borderRadius":"20rpx","background":"#fff","height":"auto"}'>
					<view :style='{"padding":"0 0 0 80rpx","margin":"0 0 40rpx","borderColor":"#23baf7","color":"#000","textAlign":"left","display":"none","background":"url(http://codegen.caihongy.cn/20241110/8dff7d1201304c20b53f3530844a8261.png) no-repeat left center","borderWidth":"0 0 0 0px","width":"100%","fontSize":"44rpx","position":"relative","borderStyle":"solid","fontWeight":"600"}'>
						<view :style='{"color":"#000","fontSize":"44rpx"}'>我的服务</view>
					</view>
					<view class="me-menu-view">
						<block v-for="item in menuList" v-bind:key="item.roleName">
							<block v-if="role==item.roleName" v-bind:key="menu.menu" v-for="(menu,index) in item.backMenu">
								<block v-bind:key="child.tableName" v-for=" (child,sort) in menu.child">
									<view class="me-menu-item" v-if="child.tableName!='orders/已发货' && child.tableName!='orders/已退款' &&child.tableName!='orders/已取消' && child.tableName!='orders/未支付' && child.tableName!='orders/已支付' && child.tableName!='orders/已完成' && child.tableName!='exampaper' && child.tableName!='examquestion'&& child.tableName!='hasTranslate' " @tap="onPageTap('../'+child.tableName+'/list?userid='+user.id+'&menuJump='+child.menuJump)" hover-class="hover">
										<view class="me-menu-icon" :class="child.appFrontIcon" :style="{'color': meMenuColor[index]}"></view>
										<view class="text">{{child.menu}}</view>
										<view class="icon iconfont icon-jinru"></view>
									</view>
								</block>
							</block>
						</block>
						<view v-if="user&&user.id" @tap="onPageTap('../chat/chat')" class="me-menu-item" hover-class="hover">
							<view class="cuIcon-service me-menu-icon" :style="{'color': meMenuColor[3]}"></view>
							<view class="text">客服中心</view>
							<view class="icon iconfont icon-jinru"></view>
						</view>
						<view v-if="user&&user.id" @tap="onPageTap('../forum-my/forum-my')" class="me-menu-item" hover-class="hover">
							<view class="cuIcon-scan me-menu-icon" :style="{'color': meMenuColor[5]}"></view>
							<view class="text">我的发贴</view>
							<view class="icon iconfont icon-jinru"></view>
						</view>
						<view v-if="user&&user.id" @tap="onPageTap('../messages/list')" class="me-menu-item" hover-class="hover">
							<view class="cuIcon-message me-menu-icon" :style="{'color': meMenuColor[0]}"></view>
							<view class="text">留言反馈</view>
							<view class="icon iconfont icon-jinru"></view>
						</view>
						<view v-if="changeHasChat()" @tap="getRecordList(1)" class="me-menu-item" hover-class="hover">
							<view class="cuIcon-news me-menu-icon" :style="{'color': meMenuColor[5]}"></view>
							<view class="text">聊天记录</view>
							<view class="icon iconfont icon-jinru"></view>
						</view>
						<view v-if="user&&user.id" @tap="passwordShow()" class="me-menu-item" hover-class="hover">
							<view class="cuIcon-lock me-menu-icon" :style="{'color': meMenuColor[6]}"></view>
							<view class="text">修改密码</view>
							<view class="icon iconfont icon-jinru"></view>
						</view>
					</view>
				</view>
			</view>
			
			<!-- 推荐 -->
			<view style="width: 100%;height: 80px"></view>
		</view>
		<uni-popup class="popup-content" ref="recordPopup" type="bottom">
			<view class="z-box">
				<view class="section-content" v-for="item in recordList" :key="item.id" @click="chatClick(item)">
					<view style="display: flex;align-items: center;">
						<img :src="item.picture?baseUrl + item.picture:''" style="width: 60px;height: 60px;border-radius: 50%;object-fit: cover;"
							alt="">
						<view style="margin: 0 0 0 10px;display: flex;flex-direction: column;align-items: flex-start;">
							<view :style='{"fontSize":"14px","color":"#000","flex":"1","fontWeight":"bold"}'
								class="item-style">{{item.name}}</view>
							<view style="display: flex;align-items: center;" :style='{"color":"#666","flex":"1","fontSize":"14px","lineHeight":"1.5"}'
								class="item-style">
								<view v-if="item.notreadnum"
									style="padding: 0 5px;height: 16px;border-radius: 50%;text-align: center;line-height: 16px;font-size: 12px;background: #f00;color:#fff;width: auto;display: flex; align-items: center">
									{{item.notreadnum}}
								</view>
								{{item.content.split('/').length&&item.content.split('/')[0]=='upload'?'[图片]':item.content}}
							</view>
						</view>
					</view>
					<view>
						<button @click.stop="delChat(item)" style="width: auto;padding: 0 10px;line-height: 20px;height: 20px;font-size: 14px;background: #f93636;margin: 4px 0;color: #fff;">删除</button>
					</view>
				</view> 
				<view v-if="!recordList.length" style="padding: 30px 0;width: 100%;text-align: center;font-size: 14px;color: #666;">
					暂无聊天记录
				</view>
			</view>
		</uni-popup>
		<uni-popup class="popup-content" ref="chatPopup" type="bottom" :maskClick="true" @change="clearChat">
			<view class="popup-chat">
				<view class="chat-content" id="chat-content">
					<view v-bind:key="item.id" v-for="item in chatList">
						<div v-if="item.addtime" style="width: 100%;text-align: center;font-size: 10px;color: #666;">{{timeFormat(item.addtime)}}</div>
						<view v-if="item.uid==user.id" class="right-content">
							<view v-if="item.format==1" class="text-content">{{item.content}}</view>
							<img v-else :src="item.content?baseUrl + item.content:''" @click="preViewImg(baseUrl + item.content)"
								style="width: 100px;height: 100px;object-fit: cover;" />
							<img :src="mypic?baseUrl + mypic:''" alt=""
								style="width: 30px;border-radius: 50%;height: 30px;margin: 0 0 0 10px;object-fit: cover;" />
						</view>
						<view v-else class="left-content">
							<img :src="nowfpic?baseUrl + nowfpic:''" alt=""
								style="width: 30px;border-radius: 50%;height: 30px;margin: 0 10px 0 0;object-fit: cover;" />
							<view v-if="item.format==1" class="text-content">{{item.content}}</view>
							<img v-else :src="item.content?baseUrl + item.content:''" @click="preViewImg(baseUrl + item.content)"
								style="width: 100px;height: 100px;object-fit: cover;" />
						</view>
						<view class="clear-float"></view>
					</view>
				</view>
				<view style="padding: 0 0 20px;">
					<input v-model="chatForm.content" placeholder="请输入内容" confirm-type="send" @confirm="addChat"
						style="width: calc(100% - 20px);font-size: 14px;background: #eee;margin: 0 10px 10px;padding: 0 10px;">
					</input>
					<view style="display: flex;justify-content: center;">
						<button @click="addChat" style="width: auto;padding: 0 10px;background: #29A19C;font-size: 14px;border: none;color: #fff;">发送</button>
						<button @click="uploadSuccess" style="width: auto;padding: 0 10px;background: #0BB2C7;font-size: 14px;border: none;color: #fff;">上传图片</button>
						<button @click="closeChat" style="width: auto;padding: 0 10px;background: #c774b1;font-size: 14px;border: none;color: #fff;">返回</button>
					</view>
					
				</view>
			</view>
		</uni-popup>
		<uni-popup class="popup-content" ref="passwordPopup" type="bottom">
			<view class="passwordForm">
				<view class="passwordInput">
					<input type="password" v-model="passwordForm.mima" placeholder="原密码" />
				</view>
				<view class="passwordInput">
					<input type="password" v-model="passwordForm.newmima" placeholder="新密码" />
				</view>
				<view class="passwordInput">
					<input type="password" v-model="passwordForm.newmima1" placeholder="确认密码" />
				</view>
				<view class="passwordBtnView">
					<button class="passwordBtn" @click="updatePassword">更新</button>
				</view>
			</view>
		</uni-popup>
	</view>
</template>
<script>
	import timeMethod from '@/utils/timeMethod'
	import menu from '@/utils/menu'
	export default {
		data() {
			return {
				isH5Plus: true,
				user: {},
				tableName:'',
				role: '',
				menuList: [],
				iconArr: [
					'cuIcon-same',
					'cuIcon-deliver',
					'cuIcon-evaluate',
					'cuIcon-shop',
					'cuIcon-ticket',
					'cuIcon-cascades',
					'cuIcon-discover',
					'cuIcon-question',
					'cuIcon-pic',
					'cuIcon-filter',
					'cuIcon-footprint',
					'cuIcon-pulldown',
					'cuIcon-pullup',
					'cuIcon-moreandroid',
					'cuIcon-refund',
					'cuIcon-qrcode',
					'cuIcon-remind',
					'cuIcon-profile',
					'cuIcon-home',
					'cuIcon-message',
					'cuIcon-link',
					'cuIcon-lock',
					'cuIcon-unlock',
					'cuIcon-vip',
					'cuIcon-weibo',
					'cuIcon-activity',
					'cuIcon-friendadd',
					'cuIcon-friendfamous',
					'cuIcon-friend',
					'cuIcon-goods',
					'cuIcon-selection'
				],
				// 聊天
				recordList: [],
				nowfid: 0,
				nowfpic: '',
				nowname: '',
				nowtablename: '',
				chatList: [],
				chatForm: {
					content: ''
				},
				chatTimer: null,
				hasChatList: [
					'yonghu',
					'congyezhe',
				],
				friendList: [],
				mypic:'',
				passwordForm: {
					mima: '',
					newmima: '',
					newmima1: '',
				},
				meMenuColor: '#1dcb96,#32c8d9,#74b2fd,#1ccb96,#75b2fd,#fee232,#351c6c,#f093a9,#a7c23a,#104eff,#10441f,#a21233,#503319'.split(',')
			};
		},
		computed: {
			baseUrl() {
				return this.$base.url;
			},
		},
		async onLoad(){
			let menus = menu.list();
			this.menuList = menus;
			this.meMenuColor = this.meMenuColor.sort(()=> {
				return (0.5-Math.random());
			});
		},
		async onShow(){
            uni.removeStorageSync("useridTag");
			this.role = uni.getStorageSync("appRole");
			await this.getSession()
			this.getThumbsup()
			this.getStoreup()
			this.tableName = uni.getStorageSync("nowTable");
			let menus = menu.list();
			this.menuList = menus;
			this.mypic = uni.getStorageSync('headportrait')
			this.$forceUpdate()
		},
		methods: {
			async getSession(){
				let table = uni.getStorageSync("nowTable");
				let res = await this.$api.session(table);
				this.user = res.data;
				this.$forceUpdate()
			},
			async getThumbsup(){
				if(!this.user||!this.user.id){
					return false
				}
				let res = await this.$api.page('storeup',{userid: this.user.id,type: 21})
				this.user.thumbsnum = Number(res.data.total)
				this.$forceUpdate()
			},
			async getStoreup(){
				if(!this.user||!this.user.id){
					return false
				}
				let res = await this.$api.page('storeup',{userid: this.user.id,type: 1})
				this.user.storenum = Number(res.data.total)
				this.$forceUpdate()
			},
			loginClick(){
				uni.navigateTo({
					url: '../login/login'
				});
			},
			onPageTap(url) {
                uni.setStorageSync("useridTag",1);
				uni.navigateTo({
					url: url,
					fail: function() {
						uni.switchTab({
							url: url
						});
					}
				});
			},
			hasTranslate(){
				for(let x in this.menuList){
					if(this.menuList[x].roleName == this.role){
						for(let i in this.menuList[x].backMenu){
							if(this.menuList[x].backMenu[i].child.length) {
								for(let j in this.menuList[x].backMenu[i].child) {
									if(this.menuList[x].backMenu[i].child[j].tableName=='hasTranslate'){
										return true
									}
								}
							}
						}
					}
				}
				return false
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
			changeHasChat(){
				let table = uni.getStorageSync("nowTable")
				for(let x in this.hasChatList){
					if(this.hasChatList[x]==table){
						return true
					}
				}
				return false
			},
			async getRecordList(type=1) {
				let res = await this.$api.page2('friend',{
					uid: this.user.id,
					type: 2
				})
				this.recordList = res.data.list
				if(type==1){
					this.$refs.recordPopup.open()
				}
				
			},
			async chatClick(row) {
				if (row.type == 0) {
					return false
				}
				this.nowfid = row.fid
				this.nowfpic = row.picture
				this.nowname = row.name
				this.nowtablename = row.tablename
				await this.getChatList()
				this.$refs.chatPopup.open()
				this.$forceUpdate()
			},
			async delChat(item) {
				// #ifdef MP-WEIXIN
				item = item.$orig || item
				// #endif
				let that = this
				uni.showModal({
					title: '提示',
					content: '是否删除此聊天记录？',
					success: async function(obj) {
						if (obj.confirm) {
							let arr = []
							let brr = []
							let res = await that.$api.list('chatmessage',{page: 1,limit: 10000,uid: Number(uni.getStorageSync('appUserid')),fid: item.fid})
							if(res.data.list.length){
								for(let x in res.data.list){
									arr.push(res.data.list[x].id)
								}
							}
							res = await that.$api.list('chatmessage',{page: 1,limit: 10000,uid: item.fid,fid: Number(uni.getStorageSync('appUserid'))})
							if(res.data.list.length){
								for(let x in res.data.list){
									arr.push(res.data.list[x].id)
								}
							}
							if(arr.length){
								await that.$api.del('chatmessage',JSON.stringify(arr))
							}
							res = await that.$api.list('friend',{page: 1,limit: 10000,uid: Number(uni.getStorageSync('appUserid')),fid: item.fid})
							if(res.data.list.length){
								for(let x in res.data.list){
									brr.push(res.data.list[x].id)
								}
							}
							res = await that.$api.list('friend',{page: 1,limit: 10000,uid: item.fid,fid: Number(uni.getStorageSync('appUserid'))})
							if(res.data.list.length){
								for(let x in res.data.list){
									brr.push(res.data.list[x].id)
								}
							}
							if(brr.length){
								await that.$api.del('friend',JSON.stringify(brr))
							}
							that.$utils.msg('操作成功');
							that.getRecordList(0)
						}
					}
				})
			},
			async getChatList() {
				let res = await this.$api.mlist('chatmessage',{
					page: 1,
					limit: 1000,
					uid: this.user.id,
					fid: this.nowfid
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
			preViewImg(img){
				uni.previewImage({
					urls: [img],
					current:img
				})
			},
			clearChat(e) {
				if(!e.show){
					this.getRecordList(0)
					clearTimeout(this.chatTimer)
				}
				
			},
			closeChat(){
				this.$refs.chatPopup.close()
			},
			async uploadSuccess() {
				clearTimeout(this.chatTimer)
				let _this = this;
				await this.$api.upload(async function(obj) {
					let res = await _this.$api.page('friend', {
						uid: _this.user.id,
						fid: _this.nowfid,
						type: 2
					})
					if(!res.data.list.length){
						await _this.$api.add('friend',{
							uid: _this.user.id,
							fid: _this.nowfid,
							name: _this.nowname,
							picture: _this.nowfpic,
							type: 2,
							tablename: 'yonghu'
						})
						await _this.$api.add('friend',{
							fid: _this.user.id,
							uid: _this.nowfid,
							name: uni.getStorageSync("nickname"),
							picture: _this.mypic,
							type: 2,
							tablename: uni.getStorageSync("nowTable")
						})
					}
					await _this.$api.add('chatmessage',{
						uid: _this.user.id,
						fid: _this.nowfid,
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
					fid: this.nowfid,
					type: 2
				})
				if(!res.data.list.length){
					await this.$api.add('friend',{
						uid: this.user.id,
						fid: this.nowfid,
						name: this.nowname,
						picture: this.nowfpic,
						type: 2,
						tablename: 'yonghu'
					})
					await this.$api.add('friend',{
						fid: this.user.id,
						uid: this.nowfid,
						name: uni.getStorageSync("nickname"),
						picture: this.mypic,
						type: 2,
						tablename: uni.getStorageSync("nowTable")
					})
				}
				await this.$api.add('chatmessage',{
					uid: this.user.id,
					fid: this.nowfid,
					content: this.chatForm.content,
					format: 1
				})
				this.chatForm = {
					content: ''
				}
				this.getChatList()
			},
			passwordShow() {
				this.passwordForm = {
					mima: '',
					newmima: '',
					newmima1: '',
				}
				this.$forceUpdate()
				this.$refs.passwordPopup.open()
			},
			async updatePassword() {
				if (this.passwordForm.mima == ''){
					this.$utils.msg('原密码不能为空')
					return false
				}
				if (this.passwordForm.newmima == ''){
					this.$utils.msg('新密码不能为空')
					return false
				}
				if (this.passwordForm.newmima1 == ''){
					this.$utils.msg('确认密码不能为空')
					return false
				}
				let password = ''
				if (this.user.mima) {
					password = this.user.mima;
				} else if (this.user.password) {
					password = this.user.password;
				}
				if (this.tableName == 'yonghu') {
					if(this.passwordForm.newmima && (this.passwordForm.newmima.length<3)){
						this.$utils.msg('新密码长度不能小于3')
						return
					}
					if(this.passwordForm.newmima && (this.passwordForm.newmima.length>16)){
						this.$utils.msg('新密码长度不能大于16')
						return
					}
				}
				if (this.tableName == 'congyezhe') {
					if(this.passwordForm.newmima && (this.passwordForm.newmima.length<3)){
						this.$utils.msg('新密码长度不能小于3')
						return
					}
					if(this.passwordForm.newmima && (this.passwordForm.newmima.length>16)){
						this.$utils.msg('新密码长度不能大于16')
						return
					}
				}
				let newpassword = this.passwordForm.mima
				if(password != newpassword){
					this.$utils.msg('原密码不正确')
					return false
				}
				if (this.passwordForm.newmima != this.passwordForm.newmima1){
					this.$utils.msg('两次密码不一致')
					return false
				}
				if (this.passwordForm.mima == this.passwordForm.newmima){
					this.$utils.msg('新密码与原密码相同！')
					return false
				}
				this.user.password = this.passwordForm.newmima
				this.user.mima = this.passwordForm.newmima
				await this.$api.update(this.tableName,this.user)
				this.$utils.msg('修改密码成功,下次登录系统生效')
				this.$refs.passwordPopup.close()
				this.getSession()
			},
		}
	}
</script>

<style lang="scss" scoped>
	.content {
		height: calc(100vh - 94px);
		box-sizing: border-box;
	}
	.z-box{
		background: #fff;
		width: 100%;
		padding: 10px 0 60px;
		max-height: 60vh;
		overflow-y: scroll;
		
		.section-content {
			cursor: pointer;
			padding: 10px;
			box-shadow: 0px 4px 10px 0px rgba(0, 0, 0, 0.3);
			margin: 0 auto 20px;
			color: #333;
			background: #fff;
			display: flex;
			width: calc(100% - 20px);
			border-color: #efefef;
			border-width: 0;
			align-items: center;
			border-style: solid;
			position: relative;
			justify-content: space-between;
		}
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
	.passwordForm {
		width: 100%;
		padding: 10px 20px 60px;
		background: #fff;
	
		.passwordInput {
			background: #eee;
			margin: 0 0 10px;
			padding: 0 10px;
	
			input {
				height: 36px;
				line-height: 36px;
				font-size: 14px;
			}
		}
	
		.passwordBtnView {
			width: 100%;
			display: flex;
			align-items: center;
			justify-content: center;
			padding: 10px 0;
	
			.passwordBtn {
				padding: 0 20px;
				width: auto;
				height: 20px;
				line-height: 20px;
				font-size: 14px;
				color: #fff;
				background: #007aff;
				border: none;
				border-radius: 5px;
	
			}
		}
	}
	.me-menu-view {
		padding: 0;
		align-content: flex-start;
		background: none;
		display: flex;
		width: 100%;
		align-items: flex-start;
		flex-wrap: wrap;
		height: auto;
		.me-menu-item {
			padding: 0 20rpx 10rpx;
			margin: 0 10rpx 20rpx;
			background: none;
			display: flex;
			width: 100%;
			border-color: #e7e7e7;
			border-width: 0 0 2rpx;
			align-items: center;
			position: relative;
			border-style: solid;
			height: auto;
			.me-menu-icon {
				color: rgba(0, 186, 189, 1);
				font-size: 60rpx;
				line-height: 1;
			}
			.text {
				padding: 0 20rpx;
				color: #333;
				width: 100%;
				font-size: 28rpx;
				line-height: 60rpx;
				text-align: left;
			}
			.icon {
				color: #c5c5c5;
				top: 35%;
				font-weight: 500;
				width: 28rpx;
				font-size: 28rpx;
				line-height: 28rpx;
				position: absolute;
				right: 10rpx;
			}
		}
	}
</style>
