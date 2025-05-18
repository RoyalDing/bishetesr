<template>
<view class="content">
	<view :style='{"alignContent":"flex-start","padding":"0px 24rpx 0","borderColor":"#c0c0c0","alignItems":"flex-start","flexWrap":"wrap","background":"#fff","borderWidth":"2rpx 0 0 0","display":"flex","width":"100%","borderStyle":"solid","height":"auto"}'>
		<form :style='{"width":"100%","padding":"48rpx 0 48rpx","background":"none","display":"block","height":"auto"}' class="app-update-pv">
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class="">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">陪玩单号</view>
				<view :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"#000","borderRadius":"8rpx","flex":"1","background":"#f8fff7","width":"100%","lineHeight":"80rpx","fontSize":"28rpx"}' class="right-input">
					{{ruleForm.peiwandanhao}}
				</view>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class="">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">陪玩账号</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"30rpx","height":"80rpx"}' :disabled="ro.peiwanzhanghao" v-model="ruleForm.peiwanzhanghao" placeholder="陪玩账号"  type="text"></input>
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
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class="">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">性别</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"30rpx","height":"80rpx"}' :disabled="ro.xingbie" v-model="ruleForm.xingbie" placeholder="性别"  type="text"></input>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class="">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">游戏类别</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"30rpx","height":"80rpx"}' :disabled="ro.youxileibie" v-model="ruleForm.youxileibie" placeholder="游戏类别"  type="text"></input>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class="">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">陪玩游戏</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"30rpx","height":"80rpx"}' :disabled="ro.peiwanyouxi" v-model="ruleForm.peiwanyouxi" placeholder="陪玩游戏"  type="text"></input>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class="">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">陪玩收费</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"30rpx","height":"80rpx"}' :disabled="ro.peiwanshoufei" v-model.number="ruleForm.peiwanshoufei" placeholder="陪玩收费" type="digit"></input>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class="">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">陪玩时间</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"30rpx","height":"80rpx"}' :disabled="ro.peiwanshijian" v-model.number="ruleForm.peiwanshijian" placeholder="陪玩时间" type="number"></input>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class="">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">总费用</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"30rpx","height":"80rpx"}' disabled v-model="zongfeiyong" placeholder="总费用"></input>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class="">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">用户账号</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"30rpx","height":"80rpx"}' :disabled="ro.yonghuzhanghao" v-model="ruleForm.yonghuzhanghao" placeholder="用户账号"  type="text"></input>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class="">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">用户姓名</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"30rpx","height":"80rpx"}' :disabled="ro.yonghuxingming" v-model="ruleForm.yonghuxingming" placeholder="用户姓名"  type="text"></input>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class="">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">联系方式</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"30rpx","height":"80rpx"}' :disabled="ro.lianxifangshi" v-model="ruleForm.lianxifangshi" placeholder="联系方式"  type="text"></input>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class=" select">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">下单时间</view>
				<picker  :disabled="ro.xiadanshijian" :style='{"width":"100%","flex":"1","height":"auto"}' mode="date" :value="ruleForm.xiadanshijian" @change="xiadanshijianChange">
					<view :style='{"border":"2rpx solid #b0cb5e","padding":"0 20rpx","color":"#b0cb5e","borderRadius":"8rpx","background":"#f8fff7","width":"100%","lineHeight":"80rpx","fontSize":"28rpx"}' class="uni-input">{{ruleForm.xiadanshijian?ruleForm.xiadanshijian:"请选择下单时间"}}</view>
				</picker>
			</view>
                 
			
			<view :style='{"padding":"0","margin":"40rpx 0","flexDirection":"column","display":"flex","width":"100%","justifyContent":"center","height":"auto"}' class="btn" >
				<button :style='{"border":"0","padding":"0","margin":"0 0 40rpx 0","color":"rgb(255, 255, 255)","borderRadius":"16rpx","background":"linear-gradient(30deg, rgba(238,230,164,1) 0%, rgba(181,205,99,1) 100%)","width":"100%","lineHeight":"88rpx","fontSize":"32rpx","height":"88rpx"}' @tap="onSubmitTap" class="bg-red">提交</button>
			</view>
		</form>

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
				peiwandanhao: this.getUUID(),
				peiwanzhanghao: '',
				peiwanxingming: '',
				touxiang: '',
				xingbie: '',
				youxileibie: '',
				peiwanyouxi: '',
				peiwanshoufei: '',
				peiwanshijian: '',
				zongfeiyong: '',
				yonghuzhanghao: '',
				yonghuxingming: '',
				lianxifangshi: '',
				xiadanshijian: '',
				shhf: '',
				ispay: '',
				},
				// 登录用户信息
				user: {},
				ro:{
				   peiwandanhao : false,
				   peiwanzhanghao : false,
				   peiwanxingming : false,
				   touxiang : false,
				   xingbie : false,
				   youxileibie : false,
				   peiwanyouxi : false,
				   peiwanshoufei : false,
				   peiwanshijian : false,
				   zongfeiyong : false,
				   yonghuzhanghao : false,
				   yonghuxingming : false,
				   lianxifangshi : false,
				   xiadanshijian : false,
				   sfsh : false,
				   shhf : false,
				   ispay : false,
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
			zongfeiyong : {
				get: function () {
					let c = this.ruleForm
					let a = c.peiwanshoufei*c.peiwanshijian
					this.ruleForm.zongfeiyong = a?Number(Number(a).toFixed(2)):0
					return a?Number(Number(a).toFixed(2)):0
				}
				
			},
			baseUrl() {
				return this.$base.url;
			},



		},
		async onLoad(options) {
			if(options.virtualPay){
				this.virtualPay = true
			}
			this.ruleForm.xiadanshijian = this.$utils.getCurDate();
			let table = uni.getStorageSync("nowTable");
			// 获取用户信息
			let res = await this.$api.session(table);
			this.user = res.data;
			
			// ss读取
			this.ruleForm.yonghuzhanghao = this.user.yonghuzhanghao
			this.ro.yonghuzhanghao = true;
			this.ruleForm.yonghuxingming = this.user.yonghuxingming
			this.ro.yonghuxingming = true;
			this.ruleForm.lianxifangshi = this.user.lianxifangshi
			this.ro.lianxifangshi = true;



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
				res = await this.$api.info(`peiwandingdan`, this.ruleForm.id);
				this.ruleForm = res.data;
			}
			// 跨表
			this.cross = options.cross;
			if(options.cross){
				var obj = uni.getStorageSync('crossObj');
				for (var o in obj){
					if(o=='peiwandanhao'){
						this.ruleForm.peiwandanhao = obj[o];
						this.ro.peiwandanhao = true;
						continue;
					}
					if(o=='peiwanzhanghao'){
						this.ruleForm.peiwanzhanghao = obj[o];
						this.ro.peiwanzhanghao = true;
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
					if(o=='youxileibie'){
						this.ruleForm.youxileibie = obj[o];
						this.ro.youxileibie = true;
						continue;
					}
					if(o=='peiwanyouxi'){
						this.ruleForm.peiwanyouxi = obj[o];
						this.ro.peiwanyouxi = true;
						continue;
					}
					if(o=='peiwanshoufei'){
						this.ruleForm.peiwanshoufei = obj[o];
						this.ro.peiwanshoufei = true;
						continue;
					}
					if(o=='peiwanshijian'){
						this.ruleForm.peiwanshijian = obj[o];
						this.ro.peiwanshijian = true;
						continue;
					}
					if(o=='zongfeiyong'){
						this.ruleForm.zongfeiyong = obj[o];
						this.ro.zongfeiyong = true;
						continue;
					}
					if(o=='yonghuzhanghao'){
						this.ruleForm.yonghuzhanghao = obj[o];
						this.ro.yonghuzhanghao = true;
						continue;
					}
					if(o=='yonghuxingming'){
						this.ruleForm.yonghuxingming = obj[o];
						this.ro.yonghuxingming = true;
						continue;
					}
					if(o=='lianxifangshi'){
						this.ruleForm.lianxifangshi = obj[o];
						this.ro.lianxifangshi = true;
						continue;
					}
					if(o=='xiadanshijian'){
						this.ruleForm.xiadanshijian = obj[o];
						this.ro.xiadanshijian = true;
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
			styleChange() {
				this.$nextTick(()=>{
					// document.querySelectorAll('.app-update-pv . .uni-input-input').forEach(el=>{
					//   el.style.backgroundColor = this.addUpdateForm.input.content.backgroundColor
					// })
				})
			},

			// 多级联动参数

			xiadanshijianChange(e) {
				this.ruleForm.xiadanshijian = e.target.value;
				this.$forceUpdate();
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
				this.ruleForm.ispay = '未支付'
				if(this.ruleForm.zongfeiyong==0){
					this.$utils.msg('总费用不能为空')
					return false
				}
				if(this.ruleForm.peiwandanhao){
					this.ruleForm.peiwandanhao = String(this.ruleForm.peiwandanhao)
				}
				//跨表计算判断
				var obj;
				if((!this.ruleForm.peiwanyouxi)){
					this.$utils.msg(`陪玩游戏不能为空`);
					return
				}
				if(this.ruleForm.peiwanshoufei&&(!this.$validate.isNumber(this.ruleForm.peiwanshoufei))){
					this.$utils.msg(`陪玩收费应输入数字`);
					return
				}
				if((!this.ruleForm.peiwanshijian)){
					this.$utils.msg(`陪玩时间不能为空`);
					return
				}
				if(this.ruleForm.peiwanshijian&&(!this.$validate.isIntNumer(this.ruleForm.peiwanshijian))){
					this.$utils.msg(`陪玩时间应输入整数`);
					return
				}
				if(this.ruleForm.zongfeiyong&&(!this.$validate.isNumber(this.ruleForm.zongfeiyong))){
					this.$utils.msg(`总费用应输入数字`);
					return
				}
				if(this.ruleForm.lianxifangshi&&(!this.$validate.isMobile(this.ruleForm.lianxifangshi))){
					this.$utils.msg(`联系方式应输入手机格式`);
					return
				}
				if((!this.ruleForm.xiadanshijian)){
					this.$utils.msg(`下单时间不能为空`);
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
					let res = await this.$api.list(`peiwandingdan`, params);
					if (res.data.total >= crossoptnum) {
						this.$utils.msg(uni.getStorageSync('tips'));
						uni.removeStorageSync('crossCleanType');
						return false;
					} else {
				//跨表计算
						let oet = {}
						if(this.ruleForm.id){
							await this.$api.update(`peiwandingdan`, this.ruleForm);
						}else{
							oet = await this.$api.add(`peiwandingdan`, this.ruleForm);
						}

						this.$utils.msgBack('提交成功');
					}
				} else {
				//跨表计算
					let oet = {}
					if(this.ruleForm.id){
						await this.$api.update(`peiwandingdan`, this.ruleForm);
					}else{
						oet = await this.$api.add(`peiwandingdan`, this.ruleForm);
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
