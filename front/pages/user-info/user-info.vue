<template>
<view class="content">
	<view class="box" :style='{"alignContent":"flex-start","padding":"48rpx 24rpx 0","borderColor":"#c0c0c0","alignItems":"flex-start","flexWrap":"wrap","background":"#fff","borderWidth":"2rpx 0 0 0","display":"flex","width":"100%","borderStyle":"solid","height":"auto"}'>
		<view :style='{"width":"100%","padding":"0","background":"none","display":"block","height":"auto"}'>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' v-if="tableName=='yonghu'" class="">
				<view class="title" :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}'>用户账号</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"28rpx","height":"80rpx"}' disabled="true"  v-model="ruleForm.yonghuzhanghao" placeholder="用户账号"></input>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' v-if="tableName=='yonghu'" class="">
				<view class="title" :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}'>用户姓名</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"28rpx","height":"80rpx"}'   v-model="ruleForm.yonghuxingming" placeholder="用户姓名"></input>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' v-if="tableName=='yonghu'" @tap="yonghutouxiangTap" class="">
				<view class="title" :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}'>头像</view>
				<image :style='{"width":"80rpx","borderRadius":"100%","objectFit":"cover","display":"block","height":"80rpx"}' v-if="ruleForm.touxiang" style="margin: 0;" class="avator" :src="baseUrl+ruleForm.touxiang" mode=""></image>
				<image :style='{"width":"80rpx","borderRadius":"100%","objectFit":"cover","display":"block","height":"80rpx"}' v-else class="avator" style="margin: 0;" src="../../static/gen/upload.png" mode=""></image>
			</view>
			<view v-if="tableName=='yonghu'" :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class=" select">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">性别</view>
				<picker :style='{"width":"100%","flex":"1","height":"auto"}'  @change="yonghuxingbieChange" :value="yonghuxingbieIndex" :range="yonghuxingbieOptions">
					<view :style='{"border":"2rpx solid #b0cb5e","padding":"0 20rpx","color":"#b0cb5e","borderRadius":"8rpx","background":"#f8fff7","width":"100%","lineHeight":"80rpx","fontSize":"28rpx"}' class="uni-input picker-select-input">{{ruleForm.xingbie?ruleForm.xingbie:"请选择性别"}}</view>
				</picker>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' v-if="tableName=='yonghu'" class="">
				<view class="title" :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}'>年龄</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"28rpx","height":"80rpx"}'   v-model="ruleForm.nianling" placeholder="年龄"></input>
			</view>
			<view v-if="tableName=='yonghu'" :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class=" select">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">游戏偏爱</view>
				<view :style='{"width":"100%","flex":"1","height":"auto"}'>
                    <view :style='{"border":"2rpx solid #b0cb5e","padding":"0 20rpx","color":"#b0cb5e","borderRadius":"8rpx","background":"#f8fff7","width":"100%","lineHeight":"80rpx","fontSize":"28rpx"}' @click="yonghuyouxileibieShowPicker">{{ruleForm.youxileibie?ruleForm.youxileibie:'请选择游戏偏爱'}}</view>
				</view>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' v-if="tableName=='yonghu'" class="">
				<view class="title" :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}'>联系方式</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"28rpx","height":"80rpx"}'   v-model="ruleForm.lianxifangshi" placeholder="联系方式"></input>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' v-if="tableName=='congyezhe'" class="">
				<view class="title" :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}'>陪玩账号</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"28rpx","height":"80rpx"}' disabled="true"  v-model="ruleForm.peiwanzhanghao" placeholder="陪玩账号"></input>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' v-if="tableName=='congyezhe'" class="">
				<view class="title" :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}'>陪玩姓名</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"28rpx","height":"80rpx"}'   v-model="ruleForm.peiwanxingming" placeholder="陪玩姓名"></input>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' v-if="tableName=='congyezhe'" @tap="congyezhetouxiangTap" class="">
				<view class="title" :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}'>头像</view>
				<image :style='{"width":"80rpx","borderRadius":"100%","objectFit":"cover","display":"block","height":"80rpx"}' v-if="ruleForm.touxiang" style="margin: 0;" class="avator" :src="baseUrl+ruleForm.touxiang" mode=""></image>
				<image :style='{"width":"80rpx","borderRadius":"100%","objectFit":"cover","display":"block","height":"80rpx"}' v-else class="avator" style="margin: 0;" src="../../static/gen/upload.png" mode=""></image>
			</view>
			<view v-if="tableName=='congyezhe'" :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class=" select">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">性别</view>
				<picker :style='{"width":"100%","flex":"1","height":"auto"}'  @change="congyezhexingbieChange" :value="congyezhexingbieIndex" :range="congyezhexingbieOptions">
					<view :style='{"border":"2rpx solid #b0cb5e","padding":"0 20rpx","color":"#b0cb5e","borderRadius":"8rpx","background":"#f8fff7","width":"100%","lineHeight":"80rpx","fontSize":"28rpx"}' class="uni-input picker-select-input">{{ruleForm.xingbie?ruleForm.xingbie:"请选择性别"}}</view>
				</picker>
			</view>
			<view v-if="tableName=='congyezhe'" :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class=" select">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">工作状态</view>
				<picker :style='{"width":"100%","flex":"1","height":"auto"}'  @change="congyezhegongzuozhuangtaiChange" :value="congyezhegongzuozhuangtaiIndex" :range="congyezhegongzuozhuangtaiOptions">
					<view :style='{"border":"2rpx solid #b0cb5e","padding":"0 20rpx","color":"#b0cb5e","borderRadius":"8rpx","background":"#f8fff7","width":"100%","lineHeight":"80rpx","fontSize":"28rpx"}' class="uni-input picker-select-input">{{ruleForm.gongzuozhuangtai?ruleForm.gongzuozhuangtai:"请选择工作状态"}}</view>
				</picker>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' v-if="tableName=='congyezhe'" class="">
				<view class="title" :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}'>年龄</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"28rpx","height":"80rpx"}'   v-model="ruleForm.nianling" placeholder="年龄"></input>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' v-if="tableName=='congyezhe'" class="">
				<view class="title" :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}'>工作时间</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"28rpx","height":"80rpx"}'   v-model="ruleForm.gongzuoshijian" placeholder="工作时间"></input>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' v-if="tableName=='congyezhe'" class="">
				<view class="title" :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}'>陪玩收费(元/小时)</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"28rpx","height":"80rpx"}'   v-model="ruleForm.peiwanshoufei" placeholder="陪玩收费(元/小时)"></input>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' v-if="tableName=='congyezhe'" class="">
				<view class="title" :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}'>联系电话</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"28rpx","height":"80rpx"}'   v-model="ruleForm.lianxidianhua" placeholder="联系电话"></input>
			</view>
			<view v-if="tableName=='congyezhe'" :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' class=" select">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">擅长游戏</view>
				<view :style='{"width":"100%","flex":"1","height":"auto"}'>
                    <view :style='{"border":"2rpx solid #b0cb5e","padding":"0 20rpx","color":"#b0cb5e","borderRadius":"8rpx","background":"#f8fff7","width":"100%","lineHeight":"80rpx","fontSize":"28rpx"}' @click="congyezheyouxileibieShowPicker">{{ruleForm.youxileibie?ruleForm.youxileibie:'请选择擅长游戏'}}</view>
				</view>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' v-if="tableName=='congyezhe'" class="">
				<view class="title" :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}'>身份证</view>
				<input :style='{"border":"2rpx solid #b0cb5e","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"28rpx","height":"80rpx"}'   v-model="ruleForm.shenfenzheng" placeholder="身份证"></input>
			</view>
			<view :style='{"padding":"4rpx 0px","margin":"0 0 20rpx 0","borderColor":"#b0cb5e","alignItems":"flex-start","flexDirection":"column","display":"flex","borderRadius":"60rpx","flexWrap":"wrap","borderWidth":"0px","background":"none","width":"100%","borderStyle":"solid","height":"auto"}' v-if="tableName=='congyezhe'" class="">
				<view :style='{"width":"100%","padding":"0 20rpx 0 0","lineHeight":"80rpx","fontSize":"28rpx","color":"#333","textAlign":"left"}' class="title">个人介绍</view>
                <xia-editor ref="editor" :style='{"minHeight":"300rpx","border":"2rpx solid #b0cb5e","padding":"20rpx","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"30rpx","height":"auto"}' v-model="ruleForm.gerenjieshao" placeholder="个人介绍" @editorChange="gerenjieshaoChange"></xia-editor>
			</view>
			<view :style='{"padding":"0","margin":"40rpx 0 0","flexDirection":"column","display":"flex","width":"100%","justifyContent":"center","height":"auto"}' class="btn">
				<!-- #ifdef MP-WEIXIN -->
				<button open-type="getUserInfo" @getuserinfo="getUserInfo" class="cu-btn lg" :style='{"border":"0","padding":"0px","margin":"0 0 40rpx","color":"rgb(255, 255, 255)","borderRadius":"16rpx","background":"linear-gradient(30deg, rgba(238,230,164,1) 0%, rgba(181,205,99,1) 100%)","width":"100%","lineHeight":"88rpx","fontSize":"32rpx","height":"88rpx"}'>{{ruleForm.openid?'解绑':'绑定'}}微信</button>
				<!-- #endif -->
				<button @tap="update()" class="cu-btn lg" :style='{"border":"0","padding":"0px","margin":"0 0 40rpx","color":"rgb(255, 255, 255)","borderRadius":"16rpx","background":"linear-gradient(30deg, rgba(238,230,164,1) 0%, rgba(181,205,99,1) 100%)","width":"100%","lineHeight":"88rpx","fontSize":"32rpx","height":"88rpx"}'>保存</button>
				<button @tap="logout()" class="cu-btn lg" :style='{"border":"0px solid #1ccb96","padding":"0px","margin":"0 0 20rpx","color":"#999","borderRadius":"16rpx","background":"#ebeee2","width":"100%","lineHeight":"88rpx","fontSize":"30rpx","height":"88rpx"}'>退出登录</button>
			</view>
		</view>
        <multiple-select v-model="yonghuyouxileibieShow" :data="yonghuyouxileibieOptions" :default-selected="yonghuyouxileibies" @confirm="yonghuyouxileibieConfirm"></multiple-select>
        <multiple-select v-model="congyezheyouxileibieShow" :data="congyezheyouxileibieOptions" :default-selected="congyezheyouxileibies" @confirm="congyezheyouxileibieConfirm"></multiple-select>
        <w-picker mode="dateTime" step="1" :current="false" :hasSecond="false" @confirm="congyezheclicktimeConfirm" ref="congyezheclicktime" themeColor="#333333"></w-picker>
	</view>
</view>
</template>

<script>

    import xiaEditor from '@/components/xia-editor/xia-editor';
    import multipleSelect from "@/components/momo-multipleSelect/momo-multipleSelect";
	export default {
		data() {
			return {
				ruleForm: {
				},
				tableName:"",
				yonghuxingbieOptions: [],
				yonghuxingbieIndex: 0,
                yonghuyouxileibieOptions: [],
                yonghuyouxileibieShow:false,
                yonghuyouxileibies: [],
				congyezhexingbieOptions: [],
				congyezhexingbieIndex: 0,
				congyezhegongzuozhuangtaiOptions: [],
				congyezhegongzuozhuangtaiIndex: 0,
                congyezheyouxileibieOptions: [],
                congyezheyouxileibieShow:false,
                congyezheyouxileibies: [],
				// #ifdef MP-WEIXIN
				code: '',
				// #endif
			}
		},
        components: {
            multipleSelect,
			xiaEditor
        },
		computed: {
			baseUrl() {
				return this.$base.url;
			}
		},
		async onLoad() {
			let table = uni.getStorageSync("nowTable");
			let that = this
			let res = {}
			this.tableName = table;
			this.getSession()
			// 自定义下拉框值
			if(this.tableName=='yonghu'){
				this.yonghuxingbieOptions = "男,女".split(',');
				this.yonghuxingbieOptions.forEach((item, index) => {
					if(item==this.ruleForm.xingbie) {
						this.yonghuxingbieIndex = index;
					}
				});
			}
			// 下拉框
			if(this.tableName=='yonghu'){
				res = await this.$api.option(`youxileibie`,`youxileibie`,{});
                let arr = []
                for (let x in res.data) {
                    arr.push({
                        label: res.data[x],
                        value:res.data[x]
                    })
                }
                this.yonghuyouxileibieOptions = arr;
				res = await this.$api.session(table);
				if(res.data.youxileibie){
				    let brr = res.data.youxileibie.split(',');
				    brr.forEach(item=>{
				        for(let a in this.yonghuyouxileibieOptions){
				            if(this.yonghuyouxileibieOptions[a].label == item){
				                this.yonghuyouxileibies.push(this.yonghuyouxileibieOptions[a].value);
				            }
				        }
				    })
				}
			}
            
			// 自定义下拉框值
			if(this.tableName=='congyezhe'){
				this.congyezhexingbieOptions = "男,女".split(',');
				this.congyezhexingbieOptions.forEach((item, index) => {
					if(item==this.ruleForm.xingbie) {
						this.congyezhexingbieIndex = index;
					}
				});
			}
			// 自定义下拉框值
			if(this.tableName=='congyezhe'){
				this.congyezhegongzuozhuangtaiOptions = "未上线,已上线".split(',');
				this.congyezhegongzuozhuangtaiOptions.forEach((item, index) => {
					if(item==this.ruleForm.gongzuozhuangtai) {
						this.congyezhegongzuozhuangtaiIndex = index;
					}
				});
			}
			// 下拉框
			if(this.tableName=='congyezhe'){
				res = await this.$api.option(`youxileibie`,`youxileibie`,{});
                let arr = []
                for (let x in res.data) {
                    arr.push({
                        label: res.data[x],
                        value:res.data[x]
                    })
                }
                this.congyezheyouxileibieOptions = arr;
				res = await this.$api.session(table);
				if(res.data.youxileibie){
				    let brr = res.data.youxileibie.split(',');
				    brr.forEach(item=>{
				        for(let a in this.congyezheyouxileibieOptions){
				            if(this.congyezheyouxileibieOptions[a].label == item){
				                this.congyezheyouxileibies.push(this.congyezheyouxileibieOptions[a].value);
				            }
				        }
				    })
				}
			}
            
			// #ifdef MP-WEIXIN
			uni.login({
				provider: 'weixin',
				success(res) {
					that.code = res.code
				}
			})
			// #endif
			this.styleChange()
            this.$forceUpdate()
		},
		methods: {
			// #ifdef MP-WEIXIN
			async getUserInfo(e) {
				let that = this
				if (e.detail.errMsg === "getUserInfo:ok") {
					if(that.ruleForm.openid){
						uni.showModal({
							title: '提示',
							content: '是否解绑微信？',
							success:async (rs)=> {
								if(rs.confirm){
									let res = await that.$api.wxunbind(that.tableName)
									if(res.code==0) that.$utils.msg('解绑成功，可以再次绑定其他账号')
									that.getSession()
								}
							}
						})
						return false
					}
					uni.showModal({
						title: '提示',
						content: '是否绑定微信？',
						success:async (rs)=> {
							if(rs.confirm){
								let params = {
									code: that.code,
									encryptedData: e.detail.encryptedData,
									iv: e.detail.iv,
									rawData: e.detail.rawData,
									signature: e.detail.signature
								}
								let res = await that.$api.wxbind(that.tableName, params)
								if(res.code==0) that.$utils.msg('绑定成功，下次登录可使用微信登录')
								that.getSession()
							}
						}
					})
					
				}
			},
			// #endif
			async getSession(){
				let res = await this.$api.session(this.tableName)
				this.ruleForm = res.data;
				uni.setStorageSync('userSession',JSON.stringify(res.data))
			},
			yonghutouxiangTap() {
				let _this = this;
				this.$api.upload(function(res) {
					_this.ruleForm.touxiang = 'upload/' + res.file;
					_this.$forceUpdate();
				});
			},
            // 下拉变化
            yonghuxingbieChange(e) {
                    this.yonghuxingbieIndex = e.target.value
                    this.ruleForm.xingbie = this.yonghuxingbieOptions[this.yonghuxingbieIndex]
            },
            yonghuyouxileibieShowPicker() {
                this.yonghuyouxileibieShow = true
            },
            yonghuyouxileibieConfirm(e) {
                this.yonghuyouxileibies = e
                let arr = []
                for(let x in this.yonghuyouxileibies){
                    arr.push(this.yonghuyouxileibies[x].label)
                }
                this.ruleForm.youxileibie = arr.join(',')
                this.$forceUpdate()
            },
			congyezhetouxiangTap() {
				let _this = this;
				this.$api.upload(function(res) {
					_this.ruleForm.touxiang = 'upload/' + res.file;
					_this.$forceUpdate();
				});
			},
            // 下拉变化
            congyezhexingbieChange(e) {
                    this.congyezhexingbieIndex = e.target.value
                    this.ruleForm.xingbie = this.congyezhexingbieOptions[this.congyezhexingbieIndex]
            },
            // 下拉变化
            congyezhegongzuozhuangtaiChange(e) {
                    this.congyezhegongzuozhuangtaiIndex = e.target.value
                    this.ruleForm.gongzuozhuangtai = this.congyezhegongzuozhuangtaiOptions[this.congyezhegongzuozhuangtaiIndex]
            },
            congyezheyouxileibieShowPicker() {
                this.congyezheyouxileibieShow = true
            },
            congyezheyouxileibieConfirm(e) {
                this.congyezheyouxileibies = e
                let arr = []
                for(let x in this.congyezheyouxileibies){
                    arr.push(this.congyezheyouxileibies[x].label)
                }
                this.ruleForm.youxileibie = arr.join(',')
                this.$forceUpdate()
            },
            gerenjieshaoChange(e) {
                this.ruleForm.gerenjieshao = e
            },
            // 日长控件选择日期时间
            congyezheclicktimeConfirm(val) {
                this.ruleForm.clicktime = val.result;
                this.$forceUpdate();
            },

            toggleTab(str) {
                this.$refs[str].show();
            },

			styleChange() {
				this.$nextTick(()=>{
					// document.querySelectorAll('. .uni-input-input').forEach(el=>{
					//   el.style.backgroundColor = this.userInfoForm.list.input.backgroundColor
					// })
				})
			},
			// 获取uuid
			getUUID () {
				return new Date().getTime();
			},
			logout() {
				uni.clearStorageSync()
				this.$utils.jump('../login/login');
			},
			// 注册
			async update() {

				if((!this.ruleForm.yonghuzhanghao) && `yonghu` == this.tableName){
					this.$utils.msg(`用户账号不能为空`);
					return
				}

				if((!this.ruleForm.mima) && `yonghu` == this.tableName){
					this.$utils.msg(`密码不能为空`);
					return
				}

				if((!this.ruleForm.yonghuxingming) && `yonghu` == this.tableName){
					this.$utils.msg(`用户姓名不能为空`);
					return
				}



				if(`yonghu` == this.tableName && this.ruleForm.nianling&&(!this.$validate.isIntNumer(this.ruleForm.nianling))){
					this.$utils.msg(`年龄应输入整数`);
					return
				}


				if(`yonghu` == this.tableName && this.ruleForm.lianxifangshi&&(!this.$validate.isMobile(this.ruleForm.lianxifangshi))){
					this.$utils.msg(`联系方式应输入手机格式`);
					return
				}

				if(`yonghu` == this.tableName && this.ruleForm.status&&(!this.$validate.isIntNumer(this.ruleForm.status))){
					this.$utils.msg(`状态应输入整数`);
					return
				}

				if(`yonghu` == this.tableName && this.ruleForm.passwordwrongnum&&(!this.$validate.isIntNumer(this.ruleForm.passwordwrongnum))){
					this.$utils.msg(`密码错误次数应输入整数`);
					return
				}




				if((!this.ruleForm.peiwanzhanghao) && `congyezhe` == this.tableName){
					this.$utils.msg(`陪玩账号不能为空`);
					return
				}

				if((!this.ruleForm.mima) && `congyezhe` == this.tableName){
					this.$utils.msg(`密码不能为空`);
					return
				}

				if((!this.ruleForm.peiwanxingming) && `congyezhe` == this.tableName){
					this.$utils.msg(`陪玩姓名不能为空`);
					return
				}




				if(`congyezhe` == this.tableName && this.ruleForm.nianling&&(!this.$validate.isIntNumer(this.ruleForm.nianling))){
					this.$utils.msg(`年龄应输入整数`);
					return
				}


				if((!this.ruleForm.peiwanshoufei) && `congyezhe` == this.tableName){
					this.$utils.msg(`陪玩收费(元/小时)不能为空`);
					return
				}
				if(`congyezhe` == this.tableName && this.ruleForm.peiwanshoufei&&(!this.$validate.isNumber(this.ruleForm.peiwanshoufei))){
					this.$utils.msg(`陪玩收费(元/小时)应输入数字`);
					return
				}

				if(`congyezhe` == this.tableName && this.ruleForm.lianxidianhua&&(!this.$validate.isMobile(this.ruleForm.lianxidianhua))){
					this.$utils.msg(`联系电话应输入手机格式`);
					return
				}



				if(`congyezhe` == this.tableName && this.ruleForm.shenfenzheng&&(!this.$validate.checkIdCard(this.ruleForm.shenfenzheng))){
					this.$utils.msg(`身份证应输入身份证格式`);
					return
				}

				if(`congyezhe` == this.tableName && this.ruleForm.thumbsupnum&&(!this.$validate.isIntNumer(this.ruleForm.thumbsupnum))){
					this.$utils.msg(`赞应输入整数`);
					return
				}

				if(`congyezhe` == this.tableName && this.ruleForm.crazilynum&&(!this.$validate.isIntNumer(this.ruleForm.crazilynum))){
					this.$utils.msg(`踩应输入整数`);
					return
				}


				if(`congyezhe` == this.tableName && this.ruleForm.clicknum&&(!this.$validate.isIntNumer(this.ruleForm.clicknum))){
					this.$utils.msg(`点击次数应输入整数`);
					return
				}

				if(`congyezhe` == this.tableName && this.ruleForm.storeupnum&&(!this.$validate.isIntNumer(this.ruleForm.storeupnum))){
					this.$utils.msg(`收藏数应输入整数`);
					return
				}

				if(`congyezhe` == this.tableName && this.ruleForm.status&&(!this.$validate.isIntNumer(this.ruleForm.status))){
					this.$utils.msg(`状态应输入整数`);
					return
				}

				if(`congyezhe` == this.tableName && this.ruleForm.passwordwrongnum&&(!this.$validate.isIntNumer(this.ruleForm.passwordwrongnum))){
					this.$utils.msg(`密码错误次数应输入整数`);
					return
				}



				let table = uni.getStorageSync("nowTable");
				await this.$api.update(table, this.ruleForm);
				this.$utils.msgBack('修改成功');;
				this.getSession()
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
