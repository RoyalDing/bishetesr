<template>
<view class="content">
	<view :style='{"alignContent":"flex-start","padding":"0px 24rpx 0","borderColor":"#c0c0c0","alignItems":"flex-start","flexWrap":"wrap","background":"#fff","borderWidth":"2rpx 0 0 0","display":"flex","width":"100%","borderStyle":"solid","height":"auto"}'>
		<form :style='{"width":"100%","padding":"48rpx 0 48rpx","background":"none","display":"block","height":"auto"}' class="app-update-pv">
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class="">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">表名</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"30rpx","height":"80rpx"}' :disabled="ro.tablename" v-model="ruleForm.tablename" placeholder="表名"  type="text"></input>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class="">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">名称</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"30rpx","height":"80rpx"}' :disabled="ro.name" v-model="ruleForm.name" placeholder="名称"  type="text"></input>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class="" @tap="pictureTap">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">图片</view>
				<image :style='{"width":"80rpx","borderRadius":"100%","objectFit":"cover","display":"block","height":"80rpx"}' class="avator" v-if="ruleForm.picture" :src="baseUrl+ruleForm.picture.split(',')[0]" mode="aspectFill"></image>
				<image :style='{"width":"80rpx","borderRadius":"100%","objectFit":"cover","display":"block","height":"80rpx"}' class="avator" v-else src="../../static/gen/upload.png" mode="aspectFill"></image>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class="">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">类型</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"30rpx","height":"80rpx"}' :disabled="ro.type" v-model="ruleForm.type" placeholder="类型"  type="text"></input>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class="">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">推荐类型</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"30rpx","height":"80rpx"}' :disabled="ro.inteltype" v-model="ruleForm.inteltype" placeholder="推荐类型"  type="text"></input>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class="">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">备注</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"30rpx","height":"80rpx"}' :disabled="ro.remark" v-model="ruleForm.remark" placeholder="备注"  type="text"></input>
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
				userid: '',
				refid: '',
				tablename: '',
				name: '',
				picture: '',
				type: '',
				inteltype: '',
				remark: '',
				},
				// 登录用户信息
				user: {},
				ro:{
				   userid : false,
				   refid : false,
				   tablename : false,
				   name : false,
				   picture : false,
				   type : false,
				   inteltype : false,
				   remark : false,
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
				res = await this.$api.info(`storeup`, this.ruleForm.id);
				this.ruleForm = res.data;
			}
			// 跨表
			this.cross = options.cross;
			if(options.cross){
				var obj = uni.getStorageSync('crossObj');
				for (var o in obj){
					if(o=='userid'){
						this.ruleForm.userid = obj[o];
						this.ro.userid = true;
						continue;
					}
					if(o=='refid'){
						this.ruleForm.refid = obj[o];
						this.ro.refid = true;
						continue;
					}
					if(o=='tablename'){
						this.ruleForm.tablename = obj[o];
						this.ro.tablename = true;
						continue;
					}
					if(o=='name'){
						this.ruleForm.name = obj[o];
						this.ro.name = true;
						continue;
					}
					if(o=='picture'){
						this.ruleForm.picture = obj[o].split(",")[0];
						this.ro.picture = true;
						continue;
					}
					if(o=='type'){
						this.ruleForm.type = obj[o];
						this.ro.type = true;
						continue;
					}
					if(o=='inteltype'){
						this.ruleForm.inteltype = obj[o];
						this.ro.inteltype = true;
						continue;
					}
					if(o=='remark'){
						this.ruleForm.remark = obj[o];
						this.ro.remark = true;
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




			pictureTap() {
				let _this = this;
				this.$api.upload(function(res) {
					_this.ruleForm.picture = 'upload/' + res.file;
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
				if((!this.ruleForm.userid)){
					this.$utils.msg(`用户id不能为空`);
					return
				}
				if((!this.ruleForm.name)){
					this.$utils.msg(`名称不能为空`);
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
					let res = await this.$api.list(`storeup`, params);
					if (res.data.total >= crossoptnum) {
						this.$utils.msg(uni.getStorageSync('tips'));
						uni.removeStorageSync('crossCleanType');
						return false;
					} else {
				//跨表计算
						let oet = {}
						if(this.ruleForm.id){
							await this.$api.update(`storeup`, this.ruleForm);
						}else{
							oet = await this.$api.add(`storeup`, this.ruleForm);
						}

						this.$utils.msgBack('提交成功');
					}
				} else {
				//跨表计算
					let oet = {}
					if(this.ruleForm.id){
						await this.$api.update(`storeup`, this.ruleForm);
					}else{
						oet = await this.$api.add(`storeup`, this.ruleForm);
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
