<template>
<view class="content">
	<view :style='{"alignContent":"flex-start","padding":"0px 24rpx 0","borderColor":"#c0c0c0","alignItems":"flex-start","flexWrap":"wrap","background":"#fff","borderWidth":"2rpx 0 0 0","display":"flex","width":"100%","borderStyle":"solid","height":"auto"}'>
		<form :style='{"width":"100%","padding":"48rpx 0 48rpx","background":"none","display":"block","height":"auto"}' class="app-update-pv">
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class="">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">陪玩账号</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"30rpx","height":"80rpx"}' :disabled="ro.peiwanzhanghao" v-model="ruleForm.peiwanzhanghao" placeholder="陪玩账号"  type="text"></input>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class="">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">密码</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"30rpx","height":"80rpx"}' :disabled="ro.mima" v-model="ruleForm.mima" placeholder="密码"  type="text"></input>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class="">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">陪玩姓名</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"30rpx","height":"80rpx"}' :disabled="ro.peiwanxingming" v-model="ruleForm.peiwanxingming" placeholder="陪玩姓名"  type="text"></input>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class="" @tap="touxiangTap">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">头像</view>
				<image :style='{"width":"80rpx","borderRadius":"100%","objectFit":"cover","display":"block","height":"80rpx"}' class="avator" v-if="ruleForm.touxiang" :src="baseUrl+ruleForm.touxiang.split(',')[0]" mode="aspectFill"></image>
				<image :style='{"width":"80rpx","borderRadius":"100%","objectFit":"cover","display":"block","height":"80rpx"}' class="avator" v-else src="../../static/gen/upload.png" mode="aspectFill"></image>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class=" select">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">性别</view>
				<picker :disabled="ro.xingbie" :style='{"width":"100%","flex":"1","height":"auto"}' @change="xingbieChange" :value="xingbieIndex" :range="xingbieOptions">
					<view :style='{"border":"2rpx solid #b0cb5e","padding":"0 20rpx","color":"#b0cb5e","borderRadius":"8rpx","background":"#f8fff7","width":"100%","lineHeight":"80rpx","fontSize":"28rpx"}' class="uni-input">{{ruleForm.xingbie?ruleForm.xingbie:"请选择性别"}}</view>
				</picker>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class=" select">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">工作状态</view>
				<picker :disabled="ro.gongzuozhuangtai" :style='{"width":"100%","flex":"1","height":"auto"}' @change="gongzuozhuangtaiChange" :value="gongzuozhuangtaiIndex" :range="gongzuozhuangtaiOptions">
					<view :style='{"border":"2rpx solid #b0cb5e","padding":"0 20rpx","color":"#b0cb5e","borderRadius":"8rpx","background":"#f8fff7","width":"100%","lineHeight":"80rpx","fontSize":"28rpx"}' class="uni-input">{{ruleForm.gongzuozhuangtai?ruleForm.gongzuozhuangtai:"请选择工作状态"}}</view>
				</picker>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class="">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">年龄</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"30rpx","height":"80rpx"}' :disabled="ro.nianling" v-model.number="ruleForm.nianling" placeholder="年龄" type="number"></input>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class="">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">工作时间</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"30rpx","height":"80rpx"}' :disabled="ro.gongzuoshijian" v-model="ruleForm.gongzuoshijian" placeholder="工作时间"  type="text"></input>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class="">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">陪玩收费(元/小时)</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"30rpx","height":"80rpx"}' :disabled="ro.peiwanshoufei" v-model.number="ruleForm.peiwanshoufei" placeholder="陪玩收费(元/小时)" type="digit"></input>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class="">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">联系电话</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"30rpx","height":"80rpx"}' :disabled="ro.lianxidianhua" v-model="ruleForm.lianxidianhua" placeholder="联系电话"  type="text"></input>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class=" select">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">擅长游戏</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"30rpx","height":"80rpx"}' :disabled="ro.youxileibie" v-model="ruleForm.youxileibie" placeholder="擅长游戏" @click="youxileibieShowPicker"></input>
			</view>
                       
			<view :style='{"padding":"10rpx 0px","margin":"0","borderColor":"#b0cb5e","borderRadius":"40rpx","borderWidth":"0px","background":"#fff","width":"100%","borderStyle":"solid","height":"auto"}' class="">
				<view :style='{"width":"100%","lineHeight":"80rpx","fontSize":"28rpx","color":"#666","fontWeight":"500"}' class="title">个人介绍</view>
				<xia-editor ref="gerenjieshao" :style='{"minHeight":"300rpx","border":"2rpx solid #b0cb5e","padding":"20rpx","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"30rpx","height":"auto"}' v-model="ruleForm.gerenjieshao" placeholder="个人介绍" @editorChange="gerenjieshaoChange"></xia-editor>
			</view>
			
			<view :style='{"padding":"0","margin":"40rpx 0","flexDirection":"column","display":"flex","width":"100%","justifyContent":"center","height":"auto"}' class="btn" >
				<button :style='{"border":"0","padding":"0","margin":"0 0 40rpx 0","color":"rgb(255, 255, 255)","borderRadius":"16rpx","background":"linear-gradient(30deg, rgba(238,230,164,1) 0%, rgba(181,205,99,1) 100%)","width":"100%","lineHeight":"88rpx","fontSize":"32rpx","height":"88rpx"}' @tap="onSubmitTap" class="bg-red">提交</button>
			</view>
		</form>

		<multiple-select v-model="youxileibieShow" :data="youxileibieOptions" :default-selected="ruleForm.youxileibies" @confirm="youxileibieConfirm"></multiple-select>
		<w-picker  mode="dateTime" step="1" :current="false" :hasSecond="false" @confirm="clicktimeConfirm" ref="clicktime" themeColor="#333333"></w-picker>
	</view>
</view>
</template>

<script>
	import wPicker from "@/components/w-picker/w-picker.vue";
	import xiaEditor from '@/components/xia-editor/xia-editor';
	import multipleSelect from "@/components/momo-multipleSelect/momo-multipleSelect";
	export default {
		data() {
			return {
				cross:'',
				ruleForm: {
				peiwanzhanghao: '',
				mima: '',
				peiwanxingming: '',
				touxiang: '',
				xingbie: '',
					gongzuozhuangtai: '未上线' ,
				nianling: '',
					gongzuoshijian: '8:00-24:00' ,
				peiwanshoufei: '',
				lianxidianhua: '',
				youxileibie: '',
				youxileibies: [],
				gerenjieshao: '',
				shenfenzheng: '',
				storeupnum: '',
				status: '',
				passwordwrongnum: '',
				openid: '',
				nickname: '',
				avatarurl: '',
				},
				xingbieOptions: [],
				xingbieIndex: 0,
				gongzuozhuangtaiOptions: [],
				gongzuozhuangtaiIndex: 0,
				youxileibieOptions: [],
				youxileibieShow: false,
				// 登录用户信息
				user: {},
				ro:{
				   peiwanzhanghao : false,
				   mima : false,
				   peiwanxingming : false,
				   touxiang : false,
				   xingbie : false,
				   gongzuozhuangtai : false,
				   nianling : false,
				   gongzuoshijian : false,
				   peiwanshoufei : false,
				   lianxidianhua : false,
				   youxileibie : false,
				   gerenjieshao : false,
				   shenfenzheng : false,
				   thumbsupnum : false,
				   crazilynum : false,
				   clicktime : false,
				   clicknum : false,
				   storeupnum : false,
				   status : false,
				   passwordwrongnum : false,
				   openid : false,
				   nickname : false,
				   avatarurl : false,
				},
				virtualPay: false,
			}
		},
		components: {
			wPicker,
			xiaEditor,
			multipleSelect,
		},
		computed: {
			baseUrl() {
				return this.$base.url;
			},



		},
		async onLoad(options) {
			if(options.virtualPay){
				this.virtualPay = true
			}
			let table = uni.getStorageSync("nowTable");
			// 获取用户信息
			let res = await this.$api.session(table);
			this.user = res.data;
			
			// ss读取


			// 自定义下拉框值
			this.xingbieOptions = "男,女".split(',')
			// 自定义下拉框值
			this.gongzuozhuangtaiOptions = "未上线,已上线".split(',')
			res = await this.$api.option(`youxileibie`,`youxileibie`,{});
			let youxileibieArr = []
			for (let x in res.data) {
				youxileibieArr.push({
					label: res.data[x],
					value: res.data[x]
				})
			}
			this.youxileibieOptions = youxileibieArr

			// 如果有登录，获取登录后保存的userid
			this.ruleForm.userid = uni.getStorageSync("appUserid")
			if (options.refid) {
				// 如果上一级页面传递了refid，获取改refid数据信息
				this.ruleForm.refid = Number(options.refid);
				this.ruleForm.nickname = uni.getStorageSync("nickname");
			}
			// 如果是更新操作
			if (options.id) {
				this.ruleForm.id = options.id;
				// 获取信息
				res = await this.$api.info(`congyezhe`, this.ruleForm.id);
				if (res.data.youxileibie) {
					let brr = res.data.youxileibie.split(',')
					res.data.youxileibies = []
					brr.forEach(item => {
						for (let a in this.youxileibieOptions) {
							if (this.youxileibieOptions[a].label == item) {
								res.data.youxileibies.push(this.youxileibieOptions[a].value)
							}
						}
					})
				}
				this.ruleForm = res.data;
			}
			// 跨表
			this.cross = options.cross;
			if(options.cross){
				var obj = uni.getStorageSync('crossObj');
				for (var o in obj){
					if(o=='peiwanzhanghao'){
						this.ruleForm.peiwanzhanghao = obj[o];
						this.ro.peiwanzhanghao = true;
						continue;
					}
					if(o=='mima'){
						this.ruleForm.mima = obj[o];
						this.ro.mima = true;
						continue;
					}
					if(o=='peiwanxingming'){
						this.ruleForm.peiwanxingming = obj[o];
						this.ro.peiwanxingming = true;
						continue;
					}
					if(o=='touxiang'){
						this.ruleForm.touxiang = obj[o].split(",")[0];
						this.ro.touxiang = true;
						continue;
					}
					if(o=='xingbie'){
						this.ruleForm.xingbie = obj[o];
						this.ro.xingbie = true;
						continue;
					}
					if(o=='gongzuozhuangtai'){
						this.ruleForm.gongzuozhuangtai = obj[o];
						this.ro.gongzuozhuangtai = true;
						continue;
					}
					if(o=='nianling'){
						this.ruleForm.nianling = obj[o];
						this.ro.nianling = true;
						continue;
					}
					if(o=='gongzuoshijian'){
						this.ruleForm.gongzuoshijian = obj[o];
						this.ro.gongzuoshijian = true;
						continue;
					}
					if(o=='peiwanshoufei'){
						this.ruleForm.peiwanshoufei = obj[o];
						this.ro.peiwanshoufei = true;
						continue;
					}
					if(o=='lianxidianhua'){
						this.ruleForm.lianxidianhua = obj[o];
						this.ro.lianxidianhua = true;
						continue;
					}
					if(o=='youxileibie'){
						this.ruleForm.youxileibie = obj[o];
						this.ro.youxileibie = true;
						continue;
					}
					if(o=='gerenjieshao'){
						this.ruleForm.gerenjieshao = obj[o];
						this.ro.gerenjieshao = true;
						continue;
					}
					if(o=='shenfenzheng'){
						this.ruleForm.shenfenzheng = obj[o];
						this.ro.shenfenzheng = true;
						continue;
					}
					if(o=='thumbsupnum'){
						this.ruleForm.thumbsupnum = obj[o];
						this.ro.thumbsupnum = true;
						continue;
					}
					if(o=='crazilynum'){
						this.ruleForm.crazilynum = obj[o];
						this.ro.crazilynum = true;
						continue;
					}
					if(o=='clicktime'){
						this.ruleForm.clicktime = obj[o];
						this.ro.clicktime = true;
						continue;
					}
					if(o=='clicknum'){
						this.ruleForm.clicknum = obj[o];
						this.ro.clicknum = true;
						continue;
					}
					if(o=='storeupnum'){
						this.ruleForm.storeupnum = obj[o];
						this.ro.storeupnum = true;
						continue;
					}
					if(o=='status'){
						this.ruleForm.status = obj[o];
						this.ro.status = true;
						continue;
					}
					if(o=='passwordwrongnum'){
						this.ruleForm.passwordwrongnum = obj[o];
						this.ro.passwordwrongnum = true;
						continue;
					}
					if(o=='openid'){
						this.ruleForm.openid = obj[o];
						this.ro.openid = true;
						continue;
					}
					if(o=='nickname'){
						this.ruleForm.nickname = obj[o];
						this.ro.nickname = true;
						continue;
					}
					if(o=='avatarurl'){
						this.ruleForm.avatarurl = obj[o];
						this.ro.avatarurl = true;
						continue;
					}
				}
			}
			this.styleChange()
			this.$forceUpdate()
			if (uni.getStorageSync('raffleType') && uni.getStorageSync('raffleType') != null) {
				uni.removeStorageSync('raffleType')
				setTimeout(() => {
					this.onSubmitTap()
				}, 300)
			}
		},
		methods: {
			gerenjieshaoChange(e) {
				this.ruleForm.gerenjieshao = e
			},
			styleChange() {
				this.$nextTick(()=>{
					// document.querySelectorAll('.app-update-pv . .uni-input-input').forEach(el=>{
					//   el.style.backgroundColor = this.addUpdateForm.input.content.backgroundColor
					// })
				})
			},
			youxileibieShowPicker() {
				this.youxileibieShow = true
			},
			youxileibieConfirm(e) {
				this.ruleForm.youxileibies = e
				let arr = []
				for (let x in this.ruleForm.youxileibies) {
					arr.push(this.ruleForm.youxileibies[x].label)
				}
				this.ruleForm.youxileibie = arr.join(',')
				this.$forceUpdate()
			},

			// 多级联动参数


			// 日长控件选择日期时间
			clicktimeConfirm(val) {
				console.log(val)
				this.ruleForm.clicktime = val.result;
				this.$forceUpdate();
			},

			// 下拉变化
			xingbieChange(e) {
				this.xingbieIndex = e.target.value
				this.ruleForm.xingbie = this.xingbieOptions[this.xingbieIndex]
			},
			// 下拉变化
			gongzuozhuangtaiChange(e) {
				this.gongzuozhuangtaiIndex = e.target.value
				this.ruleForm.gongzuozhuangtai = this.gongzuozhuangtaiOptions[this.gongzuozhuangtaiIndex]
			},

			touxiangTap() {
				let _this = this;
				this.$api.upload(function(res) {
					_this.ruleForm.touxiang = 'upload/' + res.file;
					_this.$forceUpdate();
					_this.$nextTick(()=>{
						_this.styleChange()
					})
				});
			},

			getUUID () {
				return new Date().getTime();
			},
			async onSubmitTap() {
				let that = this
				if((this.ruleForm.peiwanzhanghao.length<3)){
					this.$utils.msg(`陪玩账号长度不能小于3`);
					return
				}
				if((this.ruleForm.peiwanzhanghao.length>16)){
					this.$utils.msg(`陪玩账号长度不能大于16`);
					return
				}
				if((this.ruleForm.mima.length<3)){
					this.$utils.msg(`密码长度不能小于3`);
					return
				}
				if((this.ruleForm.mima.length>16)){
					this.$utils.msg(`密码长度不能大于16`);
					return
				}
				//跨表计算判断
				var obj;
				if((!this.ruleForm.peiwanzhanghao)){
					this.$utils.msg(`陪玩账号不能为空`);
					return
				}
				if((!this.ruleForm.mima)){
					this.$utils.msg(`密码不能为空`);
					return
				}
				if((!this.ruleForm.peiwanxingming)){
					this.$utils.msg(`陪玩姓名不能为空`);
					return
				}
				if(this.ruleForm.nianling&&(!this.$validate.isIntNumer(this.ruleForm.nianling))){
					this.$utils.msg(`年龄应输入整数`);
					return
				}
				if((!this.ruleForm.peiwanshoufei)){
					this.$utils.msg(`陪玩收费(元/小时)不能为空`);
					return
				}
				if(this.ruleForm.peiwanshoufei&&(!this.$validate.isNumber(this.ruleForm.peiwanshoufei))){
					this.$utils.msg(`陪玩收费(元/小时)应输入数字`);
					return
				}
				if(this.ruleForm.lianxidianhua&&(!this.$validate.isMobile(this.ruleForm.lianxidianhua))){
					this.$utils.msg(`联系电话应输入手机格式`);
					return
				}
				if(this.ruleForm.shenfenzheng&&(!this.$validate.checkIdCard(this.ruleForm.shenfenzheng))){
					this.$utils.msg(`身份证应输入身份证格式`);
					return
				}
				if(this.ruleForm.thumbsupnum&&(!this.$validate.isIntNumer(this.ruleForm.thumbsupnum))){
					this.$utils.msg(`赞应输入整数`);
					return
				}
				if(this.ruleForm.crazilynum&&(!this.$validate.isIntNumer(this.ruleForm.crazilynum))){
					this.$utils.msg(`踩应输入整数`);
					return
				}
				if(this.ruleForm.clicknum&&(!this.$validate.isIntNumer(this.ruleForm.clicknum))){
					this.$utils.msg(`点击次数应输入整数`);
					return
				}
				if(this.ruleForm.storeupnum&&(!this.$validate.isIntNumer(this.ruleForm.storeupnum))){
					this.$utils.msg(`收藏数应输入整数`);
					return
				}
				if(this.ruleForm.status&&(!this.$validate.isIntNumer(this.ruleForm.status))){
					this.$utils.msg(`状态应输入整数`);
					return
				}
				if(this.ruleForm.passwordwrongnum&&(!this.$validate.isIntNumer(this.ruleForm.passwordwrongnum))){
					this.$utils.msg(`密码错误次数应输入整数`);
					return
				}
				//更新跨表属性
				var crossuserid;
				var crossrefid;
				var crossoptnum;
				if(this.cross){
					uni.setStorageSync('crossCleanType',true);
					var statusColumnName = uni.getStorageSync('statusColumnName');
					var statusColumnValue = uni.getStorageSync('statusColumnValue');
					if(statusColumnName!='') {
						if(!obj) {
							obj = uni.getStorageSync('crossObj');
						}
						if(!statusColumnName.startsWith("[")) {
							for (var o in obj){
								if(o==statusColumnName){
									obj[o] = statusColumnValue;
								}

							}
							var table = uni.getStorageSync('crossTable');
							await this.$api.update(`${table}`, obj);
						} else {
							   crossuserid=Number(uni.getStorageSync('appUserid'));
							   crossrefid=obj['id'];
							   crossoptnum=uni.getStorageSync('statusColumnName');
							   crossoptnum=crossoptnum.replace(/\[/,"").replace(/\]/,"");
						}
					}
				}
				if(crossrefid && crossuserid) {
					this.ruleForm.crossuserid=crossuserid;
					this.ruleForm.crossrefid=crossrefid;
					let params = {
						page: 1,
						limit:10,
						crossuserid:crossuserid,
						crossrefid:crossrefid,
					}
					let res = await this.$api.list(`congyezhe`, params);
					if (res.data.total >= crossoptnum) {
						this.$utils.msg(uni.getStorageSync('tips'));
						uni.removeStorageSync('crossCleanType');
						return false;
					} else {
				//跨表计算
						let oet = {}
						if(this.ruleForm.id){
							await this.$api.update(`congyezhe`, this.ruleForm);
						}else{
							oet = await this.$api.add(`congyezhe`, this.ruleForm);
						}

						this.$utils.msgBack('提交成功');
					}
				} else {
				//跨表计算
					let oet = {}
					if(this.ruleForm.id){
						await this.$api.update(`congyezhe`, this.ruleForm);
					}else{
						oet = await this.$api.add(`congyezhe`, this.ruleForm);
					}

					this.$utils.msgBack('提交成功');
				}
			},
			optionsChange(e) {
				this.index = e.target.value
			},
			bindDateChange(e) {
				this.date = e.target.value
			},
			getDate(type) {
				const date = new Date();
				let year = date.getFullYear();
				let month = date.getMonth() + 1;
				let day = date.getDate();
				if (type === 'start') {
					year = year - 60;
				} else if (type === 'end') {
					year = year + 2;
				}
				month = month > 9 ? month : '0' + month;;
				day = day > 9 ? day : '0' + day;
				return `${year}-${month}-${day}`;
			},
			toggleTab(str) {
				if(this.ro[str]){
					return false
				}
				this.$refs[str].show();
			},
		}
	}
</script>

<style lang="scss" scoped>
	.content {
		min-height: calc(100vh - 44px);
		box-sizing: border-box;
	}
</style>
