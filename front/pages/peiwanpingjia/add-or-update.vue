<template>
<view class="content">
	<view :style='{"alignContent":"flex-start","padding":"0px 24rpx 0","borderColor":"#c0c0c0","alignItems":"flex-start","flexWrap":"wrap","background":"#fff","borderWidth":"2rpx 0 0 0","display":"flex","width":"100%","borderStyle":"solid","height":"auto"}'>
		<form :style='{"width":"100%","padding":"48rpx 0 48rpx","background":"none","display":"block","height":"auto"}' class="app-update-pv">
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class="">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">陪玩单号</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"30rpx","height":"80rpx"}' :disabled="ro.peiwandanhao" v-model="ruleForm.peiwandanhao" placeholder="陪玩单号"  type="text"></input>
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
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class=" select">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">游戏能力</view>
				<picker :disabled="ro.youxinengli" :style='{"width":"100%","flex":"1","height":"auto"}' @change="youxinengliChange" :value="youxinengliIndex" :range="youxinengliOptions">
					<view :style='{"border":"2rpx solid #b0cb5e","padding":"0 20rpx","color":"#b0cb5e","borderRadius":"8rpx","background":"#f8fff7","width":"100%","lineHeight":"80rpx","fontSize":"28rpx"}' class="uni-input">{{ruleForm.youxinengli?ruleForm.youxinengli:"请选择游戏能力"}}</view>
				</picker>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class=" select">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">陪玩态度</view>
				<picker :disabled="ro.peiwantaidu" :style='{"width":"100%","flex":"1","height":"auto"}' @change="peiwantaiduChange" :value="peiwantaiduIndex" :range="peiwantaiduOptions">
					<view :style='{"border":"2rpx solid #b0cb5e","padding":"0 20rpx","color":"#b0cb5e","borderRadius":"8rpx","background":"#f8fff7","width":"100%","lineHeight":"80rpx","fontSize":"28rpx"}' class="uni-input">{{ruleForm.peiwantaidu?ruleForm.peiwantaidu:"请选择陪玩态度"}}</view>
				</picker>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class="">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">用户账号</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"30rpx","height":"80rpx"}' :disabled="ro.yonghuzhanghao" v-model="ruleForm.yonghuzhanghao" placeholder="用户账号"  type="text"></input>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class="">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">用户姓名</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"30rpx","height":"80rpx"}' :disabled="ro.yonghuxingming" v-model="ruleForm.yonghuxingming" placeholder="用户姓名"  type="text"></input>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class=" select">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">评价日期</view>
				<picker  :disabled="ro.pingjiariqi" :style='{"width":"100%","flex":"1","height":"auto"}' mode="date" :value="ruleForm.pingjiariqi" @change="pingjiariqiChange">
					<view :style='{"border":"2rpx solid #b0cb5e","padding":"0 20rpx","color":"#b0cb5e","borderRadius":"8rpx","background":"#f8fff7","width":"100%","lineHeight":"80rpx","fontSize":"28rpx"}' class="uni-input">{{ruleForm.pingjiariqi?ruleForm.pingjiariqi:"请选择评价日期"}}</view>
				</picker>
			</view>
            
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class="">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">整体评价</view>
				<textarea :style='{"border":"2rpx solid #b0cb5e","padding":"24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"28rpx","height":"300rpx"}' v-model="ruleForm.zhengtipingjia" placeholder="整体评价" :maxlength="-1"></textarea>
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
				peiwandanhao: '',
				peiwanzhanghao: '',
				peiwanxingming: '',
				touxiang: '',
				youxinengli: '',
				peiwantaidu: '',
				zhengtipingjia: '',
				yonghuzhanghao: '',
				yonghuxingming: '',
				pingjiariqi: '',
				crossuserid: '',
				crossrefid: '',
				},
				youxinengliOptions: [],
				youxinengliIndex: 0,
				peiwantaiduOptions: [],
				peiwantaiduIndex: 0,
				// 登录用户信息
				user: {},
				ro:{
				   peiwandanhao : false,
				   peiwanzhanghao : false,
				   peiwanxingming : false,
				   touxiang : false,
				   youxinengli : false,
				   peiwantaidu : false,
				   zhengtipingjia : false,
				   yonghuzhanghao : false,
				   yonghuxingming : false,
				   pingjiariqi : false,
				   crossuserid : false,
				   crossrefid : false,
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
			this.ruleForm.pingjiariqi = this.$utils.getCurDate();
			let table = uni.getStorageSync("nowTable");
			// 获取用户信息
			let res = await this.$api.session(table);
			this.user = res.data;
			
			// ss读取


			// 自定义下拉框值
			this.youxinengliOptions = "1星,2星,3星,4星,5星".split(',')
			// 自定义下拉框值
			this.peiwantaiduOptions = "1星,2星,3星,4星,5星".split(',')

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
				res = await this.$api.info(`peiwanpingjia`, this.ruleForm.id);
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
					if(o=='youxinengli'){
						this.ruleForm.youxinengli = obj[o];
						this.ro.youxinengli = true;
						continue;
					}
					if(o=='peiwantaidu'){
						this.ruleForm.peiwantaidu = obj[o];
						this.ro.peiwantaidu = true;
						continue;
					}
					if(o=='zhengtipingjia'){
						this.ruleForm.zhengtipingjia = obj[o];
						this.ro.zhengtipingjia = true;
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
					if(o=='pingjiariqi'){
						this.ruleForm.pingjiariqi = obj[o];
						this.ro.pingjiariqi = true;
						continue;
					}
					if(o=='crossuserid'){
						this.ruleForm.crossuserid = obj[o];
						this.ro.crossuserid = true;
						continue;
					}
					if(o=='crossrefid'){
						this.ruleForm.crossrefid = obj[o];
						this.ro.crossrefid = true;
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

			pingjiariqiChange(e) {
				this.ruleForm.pingjiariqi = e.target.value;
				this.$forceUpdate();
			},


			// 下拉变化
			youxinengliChange(e) {
				this.youxinengliIndex = e.target.value
				this.ruleForm.youxinengli = this.youxinengliOptions[this.youxinengliIndex]
			},
			// 下拉变化
			peiwantaiduChange(e) {
				this.peiwantaiduIndex = e.target.value
				this.ruleForm.peiwantaidu = this.peiwantaiduOptions[this.peiwantaiduIndex]
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
				//跨表计算判断
				var obj;
				if((!this.ruleForm.youxinengli)){
					this.$utils.msg(`游戏能力不能为空`);
					return
				}
				if((!this.ruleForm.peiwantaidu)){
					this.$utils.msg(`陪玩态度不能为空`);
					return
				}
				if((!this.ruleForm.zhengtipingjia)){
					this.$utils.msg(`整体评价不能为空`);
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
					let res = await this.$api.list(`peiwanpingjia`, params);
					if (res.data.total >= crossoptnum) {
						this.$utils.msg(uni.getStorageSync('tips'));
						uni.removeStorageSync('crossCleanType');
						return false;
					} else {
				//跨表计算
						let oet = {}
						if(this.ruleForm.id){
							await this.$api.update(`peiwanpingjia`, this.ruleForm);
						}else{
							oet = await this.$api.add(`peiwanpingjia`, this.ruleForm);
						}

						this.$utils.msgBack('提交成功');
					}
				} else {
				//跨表计算
					let oet = {}
					if(this.ruleForm.id){
						await this.$api.update(`peiwanpingjia`, this.ruleForm);
					}else{
						oet = await this.$api.add(`peiwanpingjia`, this.ruleForm);
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
