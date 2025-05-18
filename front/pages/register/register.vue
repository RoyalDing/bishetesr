<template>
<view class="content">
	<view class="box" :style='{"minHeight":"100vh","width":"100%","padding":"360rpx 0 24rpx","background":"url(http://codegen.caihongy.cn/20241123/711cc904af7e41b6958532cf815eb5f2.jpg) no-repeat center top / 100% auto,#fff","height":"auto"}'>
		<view :style='{"border":"2rpx solid #fff","padding":"120rpx 48rpx 144rpx","margin":"100rpx 0 0","textAlign":"center","display":"flex","justifyContent":"space-between","alignContent":"flex-start","borderRadius":"60rpx","flexWrap":"wrap","background":"rgba(255,255,255,1)","width":"100%","position":"relative","height":"auto"}'>
			<image :style='{"margin":"0 auto 24rpx auto","borderRadius":"20rpx","top":"-80rpx","left":"40%","display":"block","width":"160rpx","position":"absolute","height":"160rpx"}' src="http://codegen.caihongy.cn/20241123/4324dcf29ab04cd5b21575c06966a946.png" mode="aspectFill"></image>
			<view :style='{"border":"0px solid #1ccb96","margin":"0 0 48rpx 0","borderRadius":"20rpx","flexWrap":"wrap","background":"none","display":"flex","width":"calc(100% - 0px)","height":"auto"}' v-if="tableName=='yonghu'" class="uni-form-item uni-column">
				<view :style='{"padding":"0 20rpx","color":"#fff","borderRadius":"8rpx 8rpx 0 0","textAlign":"left","background":"#B0CB5E","width":"auto","lineHeight":"60rpx","fontSize":"28rpx","minWidth":"160rpx"}' class="label">用户账号：</view>
				<input :style='{"border":"2rpx solid #9D9D9D","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"0 8rpx 8rpx 8rpx","textAlign":"left","background":"#fff","width":"100%","fontSize":"28rpx","lineHeight":"88rpx","height":"88rpx"}'  v-model="ruleForm.yonghuzhanghao"  type="text"  class="uni-input" name="" placeholder="用户账号" />
			</view>
			<view :style='{"border":"0px solid #1ccb96","margin":"0 0 48rpx 0","borderRadius":"20rpx","flexWrap":"wrap","background":"none","display":"flex","width":"calc(100% - 0px)","height":"auto"}' v-if="tableName=='yonghu'" class="uni-form-item uni-column">
				<view :style='{"padding":"0 20rpx","color":"#fff","borderRadius":"8rpx 8rpx 0 0","textAlign":"left","background":"#B0CB5E","width":"auto","lineHeight":"60rpx","fontSize":"28rpx","minWidth":"160rpx"}' class="label">密码：</view>
				<input :style='{"border":"2rpx solid #9D9D9D","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"0 8rpx 8rpx 8rpx","textAlign":"left","background":"#fff","width":"100%","fontSize":"28rpx","lineHeight":"88rpx","height":"88rpx"}'  v-model="ruleForm.mima" type="password"  class="uni-input" name="" placeholder="密码" />
			</view>
			<view :style='{"border":"0px solid #1ccb96","margin":"0 0 48rpx 0","borderRadius":"20rpx","flexWrap":"wrap","background":"none","display":"flex","width":"calc(100% - 0px)","height":"auto"}' v-if="tableName=='yonghu'" class="uni-form-item uni-column">
				<view :style='{"padding":"0 20rpx","color":"#fff","borderRadius":"8rpx 8rpx 0 0","textAlign":"left","background":"#B0CB5E","width":"auto","lineHeight":"60rpx","fontSize":"28rpx","minWidth":"160rpx"}' class="label">确认密码：</view>
				<input :style='{"border":"2rpx solid #9D9D9D","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"0 8rpx 8rpx 8rpx","textAlign":"left","background":"#fff","width":"100%","fontSize":"28rpx","lineHeight":"88rpx","height":"88rpx"}' v-model="ruleForm.mima2" type="password" class="uni-input" name="" placeholder="确认密码" />
			</view>
			<view :style='{"border":"0px solid #1ccb96","margin":"0 0 48rpx 0","borderRadius":"20rpx","flexWrap":"wrap","background":"none","display":"flex","width":"calc(100% - 0px)","height":"auto"}' v-if="tableName=='yonghu'" class="uni-form-item uni-column">
				<view :style='{"padding":"0 20rpx","color":"#fff","borderRadius":"8rpx 8rpx 0 0","textAlign":"left","background":"#B0CB5E","width":"auto","lineHeight":"60rpx","fontSize":"28rpx","minWidth":"160rpx"}' class="label">用户姓名：</view>
				<input :style='{"border":"2rpx solid #9D9D9D","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"0 8rpx 8rpx 8rpx","textAlign":"left","background":"#fff","width":"100%","fontSize":"28rpx","lineHeight":"88rpx","height":"88rpx"}'  v-model="ruleForm.yonghuxingming"  type="text"  class="uni-input" name="" placeholder="用户姓名" />
			</view>
            <view :style='{"border":"0px solid #1ccb96","margin":"0 0 48rpx 0","borderRadius":"20rpx","flexWrap":"wrap","background":"none","display":"flex","width":"calc(100% - 0px)","height":"auto"}' v-if="tableName=='yonghu'" @tap="yonghutouxiangTap" class="">
				<view :style='{"padding":"0 20rpx","color":"#fff","borderRadius":"8rpx 8rpx 0 0","textAlign":"left","background":"#B0CB5E","width":"auto","lineHeight":"60rpx","fontSize":"28rpx","minWidth":"160rpx"}' class="label">头像：</view>
				<image :style='{"width":"180rpx","margin":"0px 0 0 10rpx","borderRadius":"8rpx","objectFit":"cover","display":"block","height":"80rpx"}' v-if="ruleForm.touxiang" class="avator" :src="baseUrl+ruleForm.touxiang" mode=""></image>
                <image :style='{"width":"180rpx","margin":"0px 0 0 10rpx","borderRadius":"8rpx","objectFit":"cover","display":"block","height":"80rpx"}' v-else class="avator" src="../../static/gen/upload.png" mode=""></image>
            </view>
            <view :style='{"border":"0px solid #1ccb96","margin":"0 0 48rpx 0","borderRadius":"20rpx","flexWrap":"wrap","background":"none","display":"flex","width":"calc(100% - 0px)","height":"auto"}' v-if="tableName=='yonghu'" class="">
				<view :style='{"padding":"0 20rpx","color":"#fff","borderRadius":"8rpx 8rpx 0 0","textAlign":"left","background":"#B0CB5E","width":"auto","lineHeight":"60rpx","fontSize":"28rpx","minWidth":"160rpx"}' class="label">性别：</view>
				<picker :style='{"border":"0px solid #1ccb96","margin":"0 0 24rpx 0","borderRadius":"20rpx","background":"none","display":"flex","width":"calc(100% - 0px)","height":"auto"}' v-if="tableName=='yonghu'"  @change="yonghuxingbieChange" :value="yonghuxingbieIndex" :range="yonghuxingbieOptions">
					<view>
						<view :style='{"border":"2rpx solid #9D9D9D","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"0 8rpx 8rpx 8rpx","textAlign":"left","background":"#fff","width":"100%","fontSize":"28rpx","lineHeight":"88rpx","height":"88rpx"}' class="uni-input">{{ruleForm.xingbie?ruleForm.xingbie:"请选择性别"}}</view>
					</view>
				</picker>
			</view>
			<view :style='{"border":"0px solid #1ccb96","margin":"0 0 48rpx 0","borderRadius":"20rpx","flexWrap":"wrap","background":"none","display":"flex","width":"calc(100% - 0px)","height":"auto"}' v-if="tableName=='yonghu'" class="uni-form-item uni-column">
				<view :style='{"padding":"0 20rpx","color":"#fff","borderRadius":"8rpx 8rpx 0 0","textAlign":"left","background":"#B0CB5E","width":"auto","lineHeight":"60rpx","fontSize":"28rpx","minWidth":"160rpx"}' class="label">年龄：</view>
				<input :style='{"border":"2rpx solid #9D9D9D","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"0 8rpx 8rpx 8rpx","textAlign":"left","background":"#fff","width":"100%","fontSize":"28rpx","lineHeight":"88rpx","height":"88rpx"}'  v-model="ruleForm.nianling"  type="text"  class="uni-input" name="" placeholder="年龄" />
			</view>
            <view :style='{"border":"0px solid #1ccb96","margin":"0 0 48rpx 0","borderRadius":"20rpx","flexWrap":"wrap","background":"none","display":"flex","width":"calc(100% - 0px)","height":"auto"}' v-if="tableName=='yonghu'">
				<view :style='{"padding":"0 20rpx","color":"#fff","borderRadius":"8rpx 8rpx 0 0","textAlign":"left","background":"#B0CB5E","width":"auto","lineHeight":"60rpx","fontSize":"28rpx","minWidth":"160rpx"}' class="label">游戏偏爱：</view>
				<view :style='{"border":"0px solid #1ccb96","margin":"0 0 24rpx 0","borderRadius":"20rpx","background":"none","display":"flex","width":"calc(100% - 0px)","height":"auto"}' @click="yonghuyouxileibieShowPicker">
					<view :style='{"border":"2rpx solid #9D9D9D","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"0 8rpx 8rpx 8rpx","textAlign":"left","background":"#fff","width":"100%","fontSize":"28rpx","lineHeight":"88rpx","height":"88rpx"}'>{{ruleForm.youxileibie?ruleForm.youxileibie:'请选择游戏偏爱'}}</view>
				</view>
            </view>
			<view :style='{"border":"0px solid #1ccb96","margin":"0 0 48rpx 0","borderRadius":"20rpx","flexWrap":"wrap","background":"none","display":"flex","width":"calc(100% - 0px)","height":"auto"}' v-if="tableName=='yonghu'" class="uni-form-item uni-column">
				<view :style='{"padding":"0 20rpx","color":"#fff","borderRadius":"8rpx 8rpx 0 0","textAlign":"left","background":"#B0CB5E","width":"auto","lineHeight":"60rpx","fontSize":"28rpx","minWidth":"160rpx"}' class="label">联系方式：</view>
				<input :style='{"border":"2rpx solid #9D9D9D","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"0 8rpx 8rpx 8rpx","textAlign":"left","background":"#fff","width":"100%","fontSize":"28rpx","lineHeight":"88rpx","height":"88rpx"}'  v-model="ruleForm.lianxifangshi"  type="text"  class="uni-input" name="" placeholder="联系方式" />
			</view>
			<view :style='{"border":"0px solid #1ccb96","margin":"0 0 48rpx 0","borderRadius":"20rpx","flexWrap":"wrap","background":"none","display":"flex","width":"calc(100% - 0px)","height":"auto"}' v-if="tableName=='congyezhe'" class="uni-form-item uni-column">
				<view :style='{"padding":"0 20rpx","color":"#fff","borderRadius":"8rpx 8rpx 0 0","textAlign":"left","background":"#B0CB5E","width":"auto","lineHeight":"60rpx","fontSize":"28rpx","minWidth":"160rpx"}' class="label">陪玩账号：</view>
				<input :style='{"border":"2rpx solid #9D9D9D","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"0 8rpx 8rpx 8rpx","textAlign":"left","background":"#fff","width":"100%","fontSize":"28rpx","lineHeight":"88rpx","height":"88rpx"}'  v-model="ruleForm.peiwanzhanghao"  type="text"  class="uni-input" name="" placeholder="陪玩账号" />
			</view>
			<view :style='{"border":"0px solid #1ccb96","margin":"0 0 48rpx 0","borderRadius":"20rpx","flexWrap":"wrap","background":"none","display":"flex","width":"calc(100% - 0px)","height":"auto"}' v-if="tableName=='congyezhe'" class="uni-form-item uni-column">
				<view :style='{"padding":"0 20rpx","color":"#fff","borderRadius":"8rpx 8rpx 0 0","textAlign":"left","background":"#B0CB5E","width":"auto","lineHeight":"60rpx","fontSize":"28rpx","minWidth":"160rpx"}' class="label">密码：</view>
				<input :style='{"border":"2rpx solid #9D9D9D","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"0 8rpx 8rpx 8rpx","textAlign":"left","background":"#fff","width":"100%","fontSize":"28rpx","lineHeight":"88rpx","height":"88rpx"}'  v-model="ruleForm.mima" type="password"  class="uni-input" name="" placeholder="密码" />
			</view>
			<view :style='{"border":"0px solid #1ccb96","margin":"0 0 48rpx 0","borderRadius":"20rpx","flexWrap":"wrap","background":"none","display":"flex","width":"calc(100% - 0px)","height":"auto"}' v-if="tableName=='congyezhe'" class="uni-form-item uni-column">
				<view :style='{"padding":"0 20rpx","color":"#fff","borderRadius":"8rpx 8rpx 0 0","textAlign":"left","background":"#B0CB5E","width":"auto","lineHeight":"60rpx","fontSize":"28rpx","minWidth":"160rpx"}' class="label">确认密码：</view>
				<input :style='{"border":"2rpx solid #9D9D9D","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"0 8rpx 8rpx 8rpx","textAlign":"left","background":"#fff","width":"100%","fontSize":"28rpx","lineHeight":"88rpx","height":"88rpx"}' v-model="ruleForm.mima2" type="password" class="uni-input" name="" placeholder="确认密码" />
			</view>
			<view :style='{"border":"0px solid #1ccb96","margin":"0 0 48rpx 0","borderRadius":"20rpx","flexWrap":"wrap","background":"none","display":"flex","width":"calc(100% - 0px)","height":"auto"}' v-if="tableName=='congyezhe'" class="uni-form-item uni-column">
				<view :style='{"padding":"0 20rpx","color":"#fff","borderRadius":"8rpx 8rpx 0 0","textAlign":"left","background":"#B0CB5E","width":"auto","lineHeight":"60rpx","fontSize":"28rpx","minWidth":"160rpx"}' class="label">陪玩姓名：</view>
				<input :style='{"border":"2rpx solid #9D9D9D","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"0 8rpx 8rpx 8rpx","textAlign":"left","background":"#fff","width":"100%","fontSize":"28rpx","lineHeight":"88rpx","height":"88rpx"}'  v-model="ruleForm.peiwanxingming"  type="text"  class="uni-input" name="" placeholder="陪玩姓名" />
			</view>
            <view :style='{"border":"0px solid #1ccb96","margin":"0 0 48rpx 0","borderRadius":"20rpx","flexWrap":"wrap","background":"none","display":"flex","width":"calc(100% - 0px)","height":"auto"}' v-if="tableName=='congyezhe'" @tap="congyezhetouxiangTap" class="">
				<view :style='{"padding":"0 20rpx","color":"#fff","borderRadius":"8rpx 8rpx 0 0","textAlign":"left","background":"#B0CB5E","width":"auto","lineHeight":"60rpx","fontSize":"28rpx","minWidth":"160rpx"}' class="label">头像：</view>
				<image :style='{"width":"180rpx","margin":"0px 0 0 10rpx","borderRadius":"8rpx","objectFit":"cover","display":"block","height":"80rpx"}' v-if="ruleForm.touxiang" class="avator" :src="baseUrl+ruleForm.touxiang" mode=""></image>
                <image :style='{"width":"180rpx","margin":"0px 0 0 10rpx","borderRadius":"8rpx","objectFit":"cover","display":"block","height":"80rpx"}' v-else class="avator" src="../../static/gen/upload.png" mode=""></image>
            </view>
            <view :style='{"border":"0px solid #1ccb96","margin":"0 0 48rpx 0","borderRadius":"20rpx","flexWrap":"wrap","background":"none","display":"flex","width":"calc(100% - 0px)","height":"auto"}' v-if="tableName=='congyezhe'" class="">
				<view :style='{"padding":"0 20rpx","color":"#fff","borderRadius":"8rpx 8rpx 0 0","textAlign":"left","background":"#B0CB5E","width":"auto","lineHeight":"60rpx","fontSize":"28rpx","minWidth":"160rpx"}' class="label">性别：</view>
				<picker :style='{"border":"0px solid #1ccb96","margin":"0 0 24rpx 0","borderRadius":"20rpx","background":"none","display":"flex","width":"calc(100% - 0px)","height":"auto"}' v-if="tableName=='congyezhe'"  @change="congyezhexingbieChange" :value="congyezhexingbieIndex" :range="congyezhexingbieOptions">
					<view>
						<view :style='{"border":"2rpx solid #9D9D9D","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"0 8rpx 8rpx 8rpx","textAlign":"left","background":"#fff","width":"100%","fontSize":"28rpx","lineHeight":"88rpx","height":"88rpx"}' class="uni-input">{{ruleForm.xingbie?ruleForm.xingbie:"请选择性别"}}</view>
					</view>
				</picker>
			</view>
            <view :style='{"border":"0px solid #1ccb96","margin":"0 0 48rpx 0","borderRadius":"20rpx","flexWrap":"wrap","background":"none","display":"flex","width":"calc(100% - 0px)","height":"auto"}' v-if="tableName=='congyezhe'" class="">
				<view :style='{"padding":"0 20rpx","color":"#fff","borderRadius":"8rpx 8rpx 0 0","textAlign":"left","background":"#B0CB5E","width":"auto","lineHeight":"60rpx","fontSize":"28rpx","minWidth":"160rpx"}' class="label">工作状态：</view>
				<picker :style='{"border":"0px solid #1ccb96","margin":"0 0 24rpx 0","borderRadius":"20rpx","background":"none","display":"flex","width":"calc(100% - 0px)","height":"auto"}' v-if="tableName=='congyezhe'"  @change="congyezhegongzuozhuangtaiChange" :value="congyezhegongzuozhuangtaiIndex" :range="congyezhegongzuozhuangtaiOptions">
					<view>
						<view :style='{"border":"2rpx solid #9D9D9D","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"0 8rpx 8rpx 8rpx","textAlign":"left","background":"#fff","width":"100%","fontSize":"28rpx","lineHeight":"88rpx","height":"88rpx"}' class="uni-input">{{ruleForm.gongzuozhuangtai?ruleForm.gongzuozhuangtai:"请选择工作状态"}}</view>
					</view>
				</picker>
			</view>
			<view :style='{"border":"0px solid #1ccb96","margin":"0 0 48rpx 0","borderRadius":"20rpx","flexWrap":"wrap","background":"none","display":"flex","width":"calc(100% - 0px)","height":"auto"}' v-if="tableName=='congyezhe'" class="uni-form-item uni-column">
				<view :style='{"padding":"0 20rpx","color":"#fff","borderRadius":"8rpx 8rpx 0 0","textAlign":"left","background":"#B0CB5E","width":"auto","lineHeight":"60rpx","fontSize":"28rpx","minWidth":"160rpx"}' class="label">年龄：</view>
				<input :style='{"border":"2rpx solid #9D9D9D","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"0 8rpx 8rpx 8rpx","textAlign":"left","background":"#fff","width":"100%","fontSize":"28rpx","lineHeight":"88rpx","height":"88rpx"}'  v-model="ruleForm.nianling"  type="text"  class="uni-input" name="" placeholder="年龄" />
			</view>
			<view :style='{"border":"0px solid #1ccb96","margin":"0 0 48rpx 0","borderRadius":"20rpx","flexWrap":"wrap","background":"none","display":"flex","width":"calc(100% - 0px)","height":"auto"}' v-if="tableName=='congyezhe'" class="uni-form-item uni-column">
				<view :style='{"padding":"0 20rpx","color":"#fff","borderRadius":"8rpx 8rpx 0 0","textAlign":"left","background":"#B0CB5E","width":"auto","lineHeight":"60rpx","fontSize":"28rpx","minWidth":"160rpx"}' class="label">工作时间：</view>
				<input :style='{"border":"2rpx solid #9D9D9D","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"0 8rpx 8rpx 8rpx","textAlign":"left","background":"#fff","width":"100%","fontSize":"28rpx","lineHeight":"88rpx","height":"88rpx"}'  v-model="ruleForm.gongzuoshijian"  type="text"  class="uni-input" name="" placeholder="工作时间" />
			</view>
			<view :style='{"border":"0px solid #1ccb96","margin":"0 0 48rpx 0","borderRadius":"20rpx","flexWrap":"wrap","background":"none","display":"flex","width":"calc(100% - 0px)","height":"auto"}' v-if="tableName=='congyezhe'" class="uni-form-item uni-column">
				<view :style='{"padding":"0 20rpx","color":"#fff","borderRadius":"8rpx 8rpx 0 0","textAlign":"left","background":"#B0CB5E","width":"auto","lineHeight":"60rpx","fontSize":"28rpx","minWidth":"160rpx"}' class="label">陪玩收费(元/小时)：</view>
				<input :style='{"border":"2rpx solid #9D9D9D","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"0 8rpx 8rpx 8rpx","textAlign":"left","background":"#fff","width":"100%","fontSize":"28rpx","lineHeight":"88rpx","height":"88rpx"}'  v-model="ruleForm.peiwanshoufei"  type="text"  class="uni-input" name="" placeholder="陪玩收费(元/小时)" />
			</view>
			<view :style='{"border":"0px solid #1ccb96","margin":"0 0 48rpx 0","borderRadius":"20rpx","flexWrap":"wrap","background":"none","display":"flex","width":"calc(100% - 0px)","height":"auto"}' v-if="tableName=='congyezhe'" class="uni-form-item uni-column">
				<view :style='{"padding":"0 20rpx","color":"#fff","borderRadius":"8rpx 8rpx 0 0","textAlign":"left","background":"#B0CB5E","width":"auto","lineHeight":"60rpx","fontSize":"28rpx","minWidth":"160rpx"}' class="label">联系电话：</view>
				<input :style='{"border":"2rpx solid #9D9D9D","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"0 8rpx 8rpx 8rpx","textAlign":"left","background":"#fff","width":"100%","fontSize":"28rpx","lineHeight":"88rpx","height":"88rpx"}'  v-model="ruleForm.lianxidianhua"  type="text"  class="uni-input" name="" placeholder="联系电话" />
			</view>
            <view :style='{"border":"0px solid #1ccb96","margin":"0 0 48rpx 0","borderRadius":"20rpx","flexWrap":"wrap","background":"none","display":"flex","width":"calc(100% - 0px)","height":"auto"}' v-if="tableName=='congyezhe'">
				<view :style='{"padding":"0 20rpx","color":"#fff","borderRadius":"8rpx 8rpx 0 0","textAlign":"left","background":"#B0CB5E","width":"auto","lineHeight":"60rpx","fontSize":"28rpx","minWidth":"160rpx"}' class="label">擅长游戏：</view>
				<view :style='{"border":"0px solid #1ccb96","margin":"0 0 24rpx 0","borderRadius":"20rpx","background":"none","display":"flex","width":"calc(100% - 0px)","height":"auto"}' @click="congyezheyouxileibieShowPicker">
					<view :style='{"border":"2rpx solid #9D9D9D","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"0 8rpx 8rpx 8rpx","textAlign":"left","background":"#fff","width":"100%","fontSize":"28rpx","lineHeight":"88rpx","height":"88rpx"}'>{{ruleForm.youxileibie?ruleForm.youxileibie:'请选择擅长游戏'}}</view>
				</view>
            </view>
			<view :style='{"border":"0px solid #1ccb96","margin":"0 0 48rpx 0","borderRadius":"20rpx","flexWrap":"wrap","background":"none","display":"flex","width":"calc(100% - 0px)","height":"auto"}' v-if="tableName=='congyezhe'" class="uni-form-item uni-column">
				<view :style='{"padding":"0 20rpx","color":"#fff","borderRadius":"8rpx 8rpx 0 0","textAlign":"left","background":"#B0CB5E","width":"auto","lineHeight":"60rpx","fontSize":"28rpx","minWidth":"160rpx"}' class="label">身份证：</view>
				<input :style='{"border":"2rpx solid #9D9D9D","padding":"0px 24rpx","margin":"0px","color":"rgb(0, 0, 0)","borderRadius":"0 8rpx 8rpx 8rpx","textAlign":"left","background":"#fff","width":"100%","fontSize":"28rpx","lineHeight":"88rpx","height":"88rpx"}'  v-model="ruleForm.shenfenzheng"  type="text"  class="uni-input" name="" placeholder="身份证" />
			</view>
			<view :style='{"border":"0px solid #1ccb96","margin":"0 0 48rpx 0","borderRadius":"20rpx","flexWrap":"wrap","background":"none","display":"flex","width":"calc(100% - 0px)","height":"auto"}' v-if="tableName=='congyezhe'" class="">
				<view :style='{"padding":"0 20rpx","color":"#fff","borderRadius":"8rpx 8rpx 0 0","textAlign":"left","background":"#B0CB5E","width":"auto","lineHeight":"60rpx","fontSize":"28rpx","minWidth":"160rpx"}' class="label">个人介绍：</view>
				<xia-editor ref="editor" :style='{"minHeight":"300rpx","border":"2rpx solid #b0cb5e","padding":"20rpx","borderRadius":"8rpx","background":"#f8fff7","width":"100%","fontSize":"30rpx","height":"auto"}' v-model="ruleForm.gerenjieshao" placeholder="个人介绍" @editorChange="gerenjieshaoChange"></xia-editor>
			</view>
			<button :style='{"border":"0","padding":"0 40rpx","margin":"0px auto","color":"rgb(255, 255, 255)","borderRadius":"8rpx","background":"linear-gradient(30deg, rgba(238,230,164,1) 0%, rgba(181,205,99,1) 100%)","display":"inline-block","width":"calc(45% - 0px)","lineHeight":"84rpx","fontSize":"36rpx","height":"84rpx"}' class="btn-submit" @tap="register" type="primary">注册</button>
			
			<view class="idea1" :style='{"width":"100%","background":"red","display":"none","height":"80rpx"}'>idea1</view>
			<view class="idea2" :style='{"width":"100%","background":"red","display":"none","height":"80rpx"}'>idea2</view>
			<view class="idea3" :style='{"width":"100%","background":"red","display":"none","height":"80rpx"}'>idea3</view>
		</view>
        <multiple-select v-model="yonghuyouxileibieShow" :data="yonghuyouxileibieOptions" :default-selected="yonghuyouxileibies" @confirm="yonghuyouxileibieConfirm"></multiple-select>
        <multiple-select v-model="congyezheyouxileibieShow" :data="congyezheyouxileibieOptions" :default-selected="congyezheyouxileibies" @confirm="congyezheyouxileibieConfirm"></multiple-select>
        <w-picker  mode="dateTime" step="1" :current="false" :hasSecond="false" @confirm="congyezheclicktimeConfirm" ref="congyezheclicktime" themeColor="#333333"></w-picker>
	</view>
</view>
</template>

<script>
    import multipleSelect from "@/components/momo-multipleSelect/momo-multipleSelect";
	export default {
		data() {
			return {
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
				ruleForm: {
                yonghuzhanghao: '',
                mima: '',
                yonghuxingming: '',
                touxiang: '',
                xingbie: '',
                nianling: '',
                youxileibie: '',
                lianxifangshi: '',
                status: '',
                passwordwrongnum: '',
                openid: '',
                nickname: '',
                avatarurl: '',
                peiwanzhanghao: '',
                mima: '',
                peiwanxingming: '',
                touxiang: '',
                xingbie: '',
                gongzuozhuangtai: '未上线',
                nianling: '',
                gongzuoshijian: '8:00-24:00',
                peiwanshoufei: '',
                lianxidianhua: '',
                youxileibie: '',
                gerenjieshao: '',
                shenfenzheng: '',
                storeupnum: '',
                status: '',
                passwordwrongnum: '',
                openid: '',
                nickname: '',
                avatarurl: '',
				},
				tableName:""
			}
		},
        components: {
            multipleSelect
        },
        computed: {
            baseUrl() {
                return this.$base.url;
            },
        },
		async onLoad() {
			let res = [];
			let table = uni.getStorageSync("loginTable");
            this.tableName = table;

                        // 自定义下拉框值
			if(this.tableName=='yonghu'){
                this.yonghuxingbieOptions = "男,女".split(',');
				this.ruleForm.xingbie=this.yonghuxingbieOptions[0]
			}
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
                //this.yonghuyouxileibieOptions = res.data;
			}
                        // 自定义下拉框值
			if(this.tableName=='congyezhe'){
                this.congyezhexingbieOptions = "男,女".split(',');
				this.ruleForm.xingbie=this.congyezhexingbieOptions[0]
			}
                        // 自定义下拉框值
			if(this.tableName=='congyezhe'){
                this.congyezhegongzuozhuangtaiOptions = "未上线,已上线".split(',');
				this.ruleForm.gongzuozhuangtai=this.congyezhegongzuozhuangtaiOptions[0]
			}
            if(`congyezhe` == this.tableName){
                this.ruleForm.gongzuozhuangtai='未上线'
            }
            if(`congyezhe` == this.tableName){
                this.ruleForm.gongzuoshijian='8:00-24:00'
            }
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
                //this.congyezheyouxileibieOptions = res.data;
			}
			
			this.styleChange()
		},
		methods: {

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
                this.yonghuyouxileibieShow = true;
            },
            yonghuyouxileibieConfirm(e) {
                this.yonghuyouxileibies = e;
                let arr = [];
                for(let x in this.yonghuyouxileibies){
                    arr.push(this.yonghuyouxileibies[x].label);
                }
                this.ruleForm.youxileibie = arr.join(',');
                this.$forceUpdate();
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
                this.congyezheyouxileibieShow = true;
            },
            congyezheyouxileibieConfirm(e) {
                this.congyezheyouxileibies = e;
                let arr = [];
                for(let x in this.congyezheyouxileibies){
                    arr.push(this.congyezheyouxileibies[x].label);
                }
                this.ruleForm.youxileibie = arr.join(',');
                this.$forceUpdate();
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
					// document.querySelectorAll('.uni-input .uni-input-input').forEach(el=>{
					//   el.style.backgroundColor = this.registerFrom.content.input.backgroundColor
					// })
				})
			},
			// 获取uuid
			getUUID () {
				return new Date().getTime();
			},
			// 注册
			async register() {
				
				if((!this.ruleForm.yonghuzhanghao) && `yonghu` == this.tableName){
					this.$utils.msg(`用户账号不能为空`);
					return
				}
				if(`yonghu` == this.tableName && (this.ruleForm.yonghuzhanghao.length<3)){
					this.$utils.msg(`用户账号长度不能小于3`);
					return
				}
				if(`yonghu` == this.tableName && (this.ruleForm.yonghuzhanghao.length>16)){
					this.$utils.msg(`用户账号长度不能大于16`);
					return
				}
				if((!this.ruleForm.mima) && `yonghu` == this.tableName){
					this.$utils.msg(`密码不能为空`);
					return
				}
				if(`yonghu` == this.tableName && (this.ruleForm.mima.length<3)){
					this.$utils.msg(`密码长度不能小于3`);
					return
				}
				if(`yonghu` == this.tableName && (this.ruleForm.mima.length>16)){
					this.$utils.msg(`密码长度不能大于16`);
					return
				}
                if(`yonghu` == this.tableName && (this.ruleForm.mima!=this.ruleForm.mima2)){
                    this.$utils.msg(`两次密码输入不一致`);
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
				if(`congyezhe` == this.tableName && (this.ruleForm.peiwanzhanghao.length<3)){
					this.$utils.msg(`陪玩账号长度不能小于3`);
					return
				}
				if(`congyezhe` == this.tableName && (this.ruleForm.peiwanzhanghao.length>16)){
					this.$utils.msg(`陪玩账号长度不能大于16`);
					return
				}
				if((!this.ruleForm.mima) && `congyezhe` == this.tableName){
					this.$utils.msg(`密码不能为空`);
					return
				}
				if(`congyezhe` == this.tableName && (this.ruleForm.mima.length<3)){
					this.$utils.msg(`密码长度不能小于3`);
					return
				}
				if(`congyezhe` == this.tableName && (this.ruleForm.mima.length>16)){
					this.$utils.msg(`密码长度不能大于16`);
					return
				}
                if(`congyezhe` == this.tableName && (this.ruleForm.mima!=this.ruleForm.mima2)){
                    this.$utils.msg(`两次密码输入不一致`);
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
				await this.$api.register(`${this.tableName}`, this.ruleForm);
				this.$utils.msgBack('注册成功');;
			}
		}
	}
</script>

<style lang="scss" scoped>
	.content {
		min-height: calc(100vh - 44px);
		box-sizing: border-box;
	}
</style>
