<template>
	<view class="content">
		<view :style='{"alignContent":"flex-start","borderColor":"#c0c0c0","alignItems":"flex-start","flexWrap":"wrap","background":"#fff","borderWidth":"2rpx 0 0 0","display":"flex","width":"100%","borderStyle":"solid","height":"auto"}'>
			<view class="list-swiper-4" :style='{"width":"calc(100% - 40rpx)","margin":"20rpx auto","position":"relative","height":"360rpx","order":"-1"}' @touchstart="touchStart" @touchmove="touchMove" @touchend="touchEnd">
				<view :style='{"top":"0%","borderRadius":"40rpx","left":"0%","background":"none","width":"100%","position":"absolute","height":"360rpx"}' class="item animate__animated" :class="prevNumList4 == index  ? 'animate__zoomOut' : (numList4 == index  ? 'animate__zoomIn' : '')" v-for="(swiper,index) in swiperList" :key="index" v-if="numList4 == index || prevNumList4 == index">
					<image :style='{"width":"100%","objectFit":"cover","borderRadius":"40rpx","display":"block","height":"360rpx"}' mode="aspectFill" :src="baseUrl+swiper.img" @tap="onSwiperTap(swiper)"></image>
					<view :style='{"padding":"8rpx 20rpx","margin":"-20rpx 0 0 0","transform":"translate3d(-50%, -50%, 0)","top":"50%","color":"#000","left":"50%","background":"rgba(255, 255, 255, 0.3)","display":"none","lineHeight":"1.5","fontSize":"40rpx","position":"absolute"}'>{{ swiper.title }}</view>
				</view>
				<view class="animate__navigation" :style='{"alignItems":"center","left":"0%","bottom":"20rpx","background":"rgba(0,0,0,0)","display":"flex","width":"100%","position":"absolute","justifyContent":"center","height":"40rpx"}'>
					<block v-for="(swiper,index) in swiperList" :key="index">
						<text class="navigation-item" v-if="numList4 == index" :style='{"width":"16rpx","margin":"0 4rpx","borderRadius":"100%","background":"#d6b8ff","height":"16rpx"}'></text>
						<text class="navigation-item" v-if="numList4 != index" :style='{"width":"16rpx","margin":"0 4rpx","borderRadius":"100%","background":"#fff","height":"16rpx"}'></text>
					</block>
				</view>
			</view>
			<view class="cu-bar bg-white search" :style='{"padding":"20rpx 24rpx","background":"none","display":"flex","width":"100%","position":"relative","height":"auto","order":"-1"}'>
				<picker :style='{"width":"40rpx","lineHeight":"80rpx","height":"80rpx"}' v-if="queryList.length>1" mode="selector" :range="queryList" range-key="queryName" :value="queryIndex" @change="queryChange">
					<text class="icon iconfont icon-jiantou18" :style='{"width":"40rpx","lineHeight":"80rpx","position":"absolute","color":"#b0cb5e","textAlign":"center"}'></text>
				</picker>
				<view :style='{"border":"2rpx solid #b0cb5e","margin":"0 12rpx 0 0","borderRadius":"60rpx","flex":"1","background":"#f8fff7","position":"relative","height":"88rpx"}' v-if="queryIndex==0" class="search-form round">
					<text class="icon iconfont icon-fangdajing07" :style='{"color":"rgb(153, 153, 153)","left":"0px","textAlign":"center","width":"80rpx","fontSize":"40rpx","lineHeight":"80rpx","position":"absolute","right":"0px"}'></text>
					<input placeholder-style="color: #333" :style='{"border":"0","padding":"12rpx 20rpx 12rpx 80rpx","color":"#333","borderRadius":"60rpx","background":"none","width":"100%","lineHeight":"56rpx","fontSize":"28rpx","height":"80rpx"}' v-model="searchForm.congyezhepeiwanxingming" type="text" placeholder="陪玩姓名" ></input>
				</view>
				<button :style='{"border":"0","padding":"0px","margin":"0","color":"#fff","borderRadius":"60rpx","background":"linear-gradient(30deg, rgba(238,230,164,1) 0%, rgba(181,205,99,1) 100%)","width":"136rpx","lineHeight":"88rpx","fontSize":"28rpx","height":"88rpx"}' v-if="queryIndex==0" @tap="onPageTap('congyezhe')" class="cu-btn shadow-blur round">搜索</button>
			</view>
			<!-- menu -->
			<view v-if="true" class="menu_view">
				<block v-for="(item,index1) in menuList" v-bind:key="item.roleName">
					<block v-if="index1==0" v-bind:key="index" v-for=" (menu,index) in item.frontMenu">
						<block v-bind:key="sort" v-for=" (child,sort) in menu.child">
							<block v-bind:key="sort2" v-for=" (button,sort2) in child.buttons">
								<view class="menu-item" v-if="button=='查看' && child.tableName!='yifahuodingdan' && child.tableName!='yituikuandingdan' &&child.tableName!='yiquxiaodingdan' && child.tableName!='weizhifudingdan' && child.tableName!='yizhifudingdan' && child.tableName!='yiwanchengdingdan' " @tap="onPageTap2(child.tableName)">
									<view class="iconarr" :class="child.appFrontIcon" :style="{'background':menuColor[index]}"></view>
									
									<view class="text">{{child.menu.split("列表")[0]}}</view>
								</view>
							</block>
						</block>
					</block>
				</block>
			</view>
			<!-- 商品推荐 -->
			<view class="listBox recommend" :style='{"width":"100%","padding":"0 24rpx","margin":"40rpx auto","background":"none","order":"3"}'>
				<view class="title" :style='{"padding":"0 0 0 20rpx","margin":"0","borderColor":"#23baf7","color":"#000","textAlign":"left","background":"url(http://codegen.caihongy.cn/20241123/185a7bcf8e5b4d6187b178faa6100999.png) no-repeat left center / auto 100%","borderWidth":"0 0 0 0px","width":"100%","lineHeight":"80rpx","position":"relative","borderStyle":"solid","fontWeight":"600"}'>
					<view :style='{"color":"#fff","fontSize":"32rpx"}'>从业者推荐</view>
				</view>
				<!-- 样式8 -->
				<view class="list-box style8" :style='{"width":"100%","padding":"0","margin":"0","height":"auto"}'>
					<view v-if="congyezhelist.length > 0" @tap="onDetailTap('congyezhe',congyezhelist[0].id)" class="box box1"  :style='{"width":"100%","padding":"0","margin":"0 0 20rpx","position":"relative","height":"auto"}'>
						<image :style='{"width":"100%","objectFit":"cover","display":"block","height":"320rpx"}' class="list-item-image" mode="aspectFill" v-if="congyezhelist[0].touxiang.substring(0,4)=='http'" :src="congyezhelist[0].touxiang"></image>
						<image :style='{"width":"100%","objectFit":"cover","display":"block","height":"320rpx"}' class="list-item-image" mode="aspectFill" v-else :src="congyezhelist[0].touxiang?baseUrl+congyezhelist[0].touxiang.split(',')[0]:''"></image>
						<view :style='{"width":"100%","padding":"20rpx","flexWrap":"wrap","background":"linear-gradient(270.00deg, rgb(189, 230, 243),rgb(238, 230, 164) 97.532%)","display":"flex"}'>
							<view :style='{"padding":"0 0px","margin":"0 0 10rpx 0","overflow":"hidden","whiteSpace":"nowrap","color":"#333","width":"100%","lineHeight":"1.5","fontSize":"32rpx","textOverflow":"ellipsis"}' class="title ">{{congyezhelist[0].peiwanxingming}}</view>
							<view :style='{"padding":"0 0px","margin":"0 0 10rpx 0","overflow":"hidden","whiteSpace":"nowrap","color":"#333","width":"100%","lineHeight":"1.5","fontSize":"32rpx","textOverflow":"ellipsis"}' class="title ">工作状态:{{congyezhelist[0].gongzuozhuangtai}}</view>
							<view :style='{"padding":"0 0px","margin":"0 0 10rpx 0","overflow":"hidden","whiteSpace":"nowrap","color":"#333","width":"100%","lineHeight":"1.5","fontSize":"32rpx","textOverflow":"ellipsis"}' class="title ">陪玩收费(元/小时):{{congyezhelist[0].peiwanshoufei}}</view>
							<view :style='{"padding":"0 20rpx 0 40rpx","color":"#339933","display":"inline-block","order":"11"}'>
								<text class="icon iconfont icon-shijian21" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
								<text :style='{"lineHeight":"1.5"}'>{{congyezhelist[0].addtime.split(' ')[0].replace(/\-/g,'-')}}</text>
							</view>
							<view :style='{"color":"#a7c839","padding":"0 20rpx 0 0","display":"inline-block"}'>
								<text class="icon iconfont icon-zan10" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
								<text :style='{"lineHeight":"1.5"}'>{{congyezhelist[0].thumbsupnum}}</text>
							</view>
							<view :style='{"color":"#8fb9e9","padding":"0 20rpx 0 0","display":"inline-block"}'>
								<text class="icon iconfont icon-shoucang10" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
								<text :style='{"lineHeight":"1.5"}'>{{congyezhelist[0].storeupnum}}</text>
							</view>
							<view :style='{"color":"#9d93c8","padding":"0 20rpx 0 0","display":"inline-block"}'>
								<text class="icon iconfont icon-chakan2" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
								<text :style='{"lineHeight":"1.5"}'>{{congyezhelist[0].clicknum}}</text>
							</view>
						</view>
					</view>
					<view class="list-item" :style='{"width":"100%","padding":"0","margin":"0 0 20rpx","justifyContent":"space-between","display":"flex","height":"auto"}'>
						<view v-if="congyezhelist.length > 1" @tap="onDetailTap('congyezhe',congyezhelist[1].id)" class="box box2" :style='{"width":"32%","padding":"0","margin":"0","position":"relative","height":"auto"}'>
							<image :style='{"width":"100%","objectFit":"cover","display":"block","height":"180rpx"}' class="list-item-image" mode="aspectFill" v-if="congyezhelist[1].touxiang.substring(0,4)=='http'" :src="congyezhelist[1].touxiang"></image>
							<image :style='{"width":"100%","objectFit":"cover","display":"block","height":"180rpx"}' class="list-item-image" mode="aspectFill" v-else :src="congyezhelist[1].touxiang?baseUrl+congyezhelist[1].touxiang.split(',')[0]:''"></image>
							<view :style='{"width":"100%","padding":"8rpx","flexWrap":"wrap","background":"linear-gradient(270.00deg, rgb(189, 230, 243),rgb(238, 230, 164) 97.532%)","display":"flex"}'>
								<view :style='{"padding":"0 0px","margin":"0 0 4rpx 0","overflow":"hidden","whiteSpace":"nowrap","color":"#333","width":"100%","lineHeight":"1.5","fontSize":"28rpx","textOverflow":"ellipsis"}' class="title ">{{congyezhelist[1].peiwanxingming}}</view>
								<view :style='{"padding":"0 0px","margin":"0 0 4rpx 0","overflow":"hidden","whiteSpace":"nowrap","color":"#333","width":"100%","lineHeight":"1.5","fontSize":"28rpx","textOverflow":"ellipsis"}' class="title ">工作状态:{{congyezhelist[1].gongzuozhuangtai}}</view>
								<view :style='{"padding":"0 0px","margin":"0 0 4rpx 0","overflow":"hidden","whiteSpace":"nowrap","color":"#333","width":"100%","lineHeight":"1.5","fontSize":"28rpx","textOverflow":"ellipsis"}' class="title ">陪玩收费(元/小时):{{congyezhelist[1].peiwanshoufei}}</view>
								<view :style='{"padding":"4rpx 0px","color":"#fff","borderRadius":"40rpx","textAlign":"center","background":"#8fb9e9","width":"100%","order":"11"}'>
									<text class="icon iconfont icon-shijian21" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
									<text :style='{"lineHeight":"1.5"}'>{{congyezhelist[1].addtime.split(' ')[0].replace(/\-/g,'-')}}</text>
								</view>
								<view :style='{"color":"#a7c839","padding":"0 10rpx 0 0","display":"inline-block"}'>
									<text class="icon iconfont icon-zan10" :style='{"margin":"0 0px 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
									<text :style='{"lineHeight":"1.5"}'>{{congyezhelist[1].thumbsupnum}}</text>
								</view>
								<view :style='{"color":"#8fb9e9","padding":"0 20rpx 0 0","display":"inline-block"}'>
									<text class="icon iconfont icon-shoucang10" :style='{"margin":"0 0px 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
									<text :style='{"lineHeight":"1.5"}'>{{congyezhelist[1].storeupnum}}</text>
								</view>
								<view :style='{"color":"#9d93c8","padding":"0 20rpx 0 0","display":"inline-block"}'>
									<text class="icon iconfont icon-chakan2" :style='{"margin":"0 0px 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
									<text :style='{"lineHeight":"1.5"}'>{{congyezhelist[1].clicknum}}</text>
								</view>
							</view>
						</view>
						<view v-if="congyezhelist.length > 2" @tap="onDetailTap('congyezhe',congyezhelist[2].id)" class="box box3" :style='{"width":"32%","padding":"0","margin":"0","position":"relative","height":"auto"}'>
							<image :style='{"width":"100%","objectFit":"cover","display":"block","height":"180rpx"}' class="list-item-image" mode="aspectFill" v-if="congyezhelist[2].touxiang.substring(0,4)=='http'" :src="congyezhelist[2].touxiang"></image>
							<image :style='{"width":"100%","objectFit":"cover","display":"block","height":"180rpx"}' class="list-item-image" mode="aspectFill" v-else :src="congyezhelist[2].touxiang?baseUrl+congyezhelist[2].touxiang.split(',')[0]:''"></image>
							<view :style='{"width":"100%","padding":"8rpx","flexWrap":"wrap","background":"linear-gradient(270.00deg, rgb(189, 230, 243),rgb(238, 230, 164) 97.532%)","display":"flex"}'>
								<view :style='{"padding":"0 0px","margin":"0 0 4rpx 0","overflow":"hidden","whiteSpace":"nowrap","color":"#333","width":"100%","lineHeight":"1.5","fontSize":"28rpx","textOverflow":"ellipsis"}' class="title ">{{congyezhelist[2].peiwanxingming}}</view>
								<view :style='{"padding":"0 0px","margin":"0 0 4rpx 0","overflow":"hidden","whiteSpace":"nowrap","color":"#333","width":"100%","lineHeight":"1.5","fontSize":"28rpx","textOverflow":"ellipsis"}' class="title ">工作状态:{{congyezhelist[2].gongzuozhuangtai}}</view>
								<view :style='{"padding":"0 0px","margin":"0 0 4rpx 0","overflow":"hidden","whiteSpace":"nowrap","color":"#333","width":"100%","lineHeight":"1.5","fontSize":"28rpx","textOverflow":"ellipsis"}' class="title ">陪玩收费(元/小时):{{congyezhelist[2].peiwanshoufei}}</view>
								<view :style='{"padding":"4rpx 0px","color":"#fff","borderRadius":"40rpx","textAlign":"center","background":"#8fb9e9","width":"100%","order":"11"}'>
									<text class="icon iconfont icon-shijian21" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
									<text :style='{"lineHeight":"1.5"}'>{{congyezhelist[2].addtime.split(' ')[0].replace(/\-/g,'-')}}</text>
								</view>
								<view :style='{"color":"#a7c839","padding":"0 10rpx 0 0","display":"inline-block"}'>
									<text class="icon iconfont icon-zan10" :style='{"margin":"0 0px 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
									<text :style='{"lineHeight":"1.5"}'>{{congyezhelist[2].thumbsupnum}}</text>
								</view>
								<view :style='{"color":"#8fb9e9","padding":"0 20rpx 0 0","display":"inline-block"}'>
									<text class="icon iconfont icon-shoucang10" :style='{"margin":"0 0px 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
									<text :style='{"lineHeight":"1.5"}'>{{congyezhelist[2].storeupnum}}</text>
								</view>
								<view :style='{"color":"#9d93c8","padding":"0 20rpx 0 0","display":"inline-block"}'>
									<text class="icon iconfont icon-chakan2" :style='{"margin":"0 0px 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
									<text :style='{"lineHeight":"1.5"}'>{{congyezhelist[2].clicknum}}</text>
								</view>
							</view>
						</view>
						<view v-if="congyezhelist.length > 3" @tap="onDetailTap('congyezhe',congyezhelist[3].id)" class="box box4" :style='{"width":"32%","padding":"0","margin":"0","position":"relative","height":"auto"}'>
							<image :style='{"width":"100%","objectFit":"cover","display":"block","height":"180rpx"}' class="list-item-image" mode="aspectFill" v-if="congyezhelist[3].touxiang.substring(0,4)=='http'" :src="congyezhelist[3].touxiang"></image>
							<image :style='{"width":"100%","objectFit":"cover","display":"block","height":"180rpx"}' class="list-item-image" mode="aspectFill" v-else :src="congyezhelist[3].touxiang?baseUrl+congyezhelist[3].touxiang.split(',')[0]:''"></image>
							<view :style='{"width":"100%","padding":"8rpx","flexWrap":"wrap","background":"linear-gradient(270.00deg, rgb(189, 230, 243),rgb(238, 230, 164) 97.532%)","display":"flex"}'>
								<view :style='{"padding":"0 0px","margin":"0 0 4rpx 0","overflow":"hidden","whiteSpace":"nowrap","color":"#333","width":"100%","lineHeight":"1.5","fontSize":"28rpx","textOverflow":"ellipsis"}' class="title ">{{congyezhelist[3].peiwanxingming}}</view>
								<view :style='{"padding":"0 0px","margin":"0 0 4rpx 0","overflow":"hidden","whiteSpace":"nowrap","color":"#333","width":"100%","lineHeight":"1.5","fontSize":"28rpx","textOverflow":"ellipsis"}' class="title ">工作状态:{{congyezhelist[3].gongzuozhuangtai}}</view>
								<view :style='{"padding":"0 0px","margin":"0 0 4rpx 0","overflow":"hidden","whiteSpace":"nowrap","color":"#333","width":"100%","lineHeight":"1.5","fontSize":"28rpx","textOverflow":"ellipsis"}' class="title ">陪玩收费(元/小时):{{congyezhelist[3].peiwanshoufei}}</view>
								<view :style='{"padding":"4rpx 0px","color":"#fff","borderRadius":"40rpx","textAlign":"center","background":"#8fb9e9","width":"100%","order":"11"}'>
									<text class="icon iconfont icon-shijian21" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
									<text :style='{"lineHeight":"1.5"}'>{{congyezhelist[3].addtime.split(' ')[0].replace(/\-/g,'-')}}</text>
								</view>
								<view :style='{"color":"#a7c839","padding":"0 10rpx 0 0","display":"inline-block"}'>
									<text class="icon iconfont icon-zan10" :style='{"margin":"0 0px 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
									<text :style='{"lineHeight":"1.5"}'>{{congyezhelist[3].thumbsupnum}}</text>
								</view>
								<view :style='{"color":"#8fb9e9","padding":"0 20rpx 0 0","display":"inline-block"}'>
									<text class="icon iconfont icon-shoucang10" :style='{"margin":"0 0px 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
									<text :style='{"lineHeight":"1.5"}'>{{congyezhelist[3].storeupnum}}</text>
								</view>
								<view :style='{"color":"#9d93c8","padding":"0 20rpx 0 0","display":"inline-block"}'>
									<text class="icon iconfont icon-chakan2" :style='{"margin":"0 0px 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
									<text :style='{"lineHeight":"1.5"}'>{{congyezhelist[3].clicknum}}</text>
								</view>
							</view>
						</view>
					</view>
					<view class="list-item" :style='{"width":"100%","padding":"0","margin":"0","justifyContent":"space-between","display":"flex","height":"auto"}'>
						<view v-if="congyezhelist.length > 4" @tap="onDetailTap('congyezhe',congyezhelist[4].id)" class="box box5" :style='{"width":"49%","padding":"0","margin":"0","position":"relative","height":"auto"}'>
							<image :style='{"width":"100%","objectFit":"cover","display":"block","height":"240rpx"}' class="list-item-image" mode="aspectFill" v-if="congyezhelist[4].touxiang.substring(0,4)=='http'" :src="congyezhelist[4].touxiang"></image>
							<image :style='{"width":"100%","objectFit":"cover","display":"block","height":"240rpx"}' class="list-item-image" mode="aspectFill" v-else :src="congyezhelist[4].touxiang?baseUrl+congyezhelist[4].touxiang.split(',')[0]:''"></image>
							<view :style='{"width":"100%","padding":"12rpx","flexWrap":"wrap","background":"linear-gradient(270.00deg, rgb(189, 230, 243),rgb(238, 230, 164) 97.532%)","display":"flex"}'>
								<view :style='{"padding":"0 0px","margin":"0 0 4rpx 0","overflow":"hidden","whiteSpace":"nowrap","color":"#333","width":"100%","lineHeight":"1.5","fontSize":"28rpx","textOverflow":"ellipsis"}' class="title ">{{congyezhelist[4].peiwanxingming}}</view>
								<view :style='{"padding":"0 0px","margin":"0 0 4rpx 0","overflow":"hidden","whiteSpace":"nowrap","color":"#333","width":"100%","lineHeight":"1.5","fontSize":"28rpx","textOverflow":"ellipsis"}' class="title ">工作状态:{{congyezhelist[4].gongzuozhuangtai}}</view>
								<view :style='{"padding":"0 0px","margin":"0 0 4rpx 0","overflow":"hidden","whiteSpace":"nowrap","color":"#333","width":"100%","lineHeight":"1.5","fontSize":"28rpx","textOverflow":"ellipsis"}' class="title ">陪玩收费(元/小时):{{congyezhelist[4].peiwanshoufei}}</view>
								<view :style='{"padding":"4rpx 0px","color":"#fff","borderRadius":"40rpx","textAlign":"center","background":"#8fb9e9","width":"100%","order":"11"}'>
									<text class="icon iconfont icon-shijian21" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
									<text :style='{"lineHeight":"1.5"}'>{{congyezhelist[4].addtime.split(' ')[0].replace(/\-/g,'-')}}</text>
								</view>
								<view :style='{"color":"#a7c839","padding":"0 20rpx 0 0","display":"inline-block"}'>
									<text class="icon iconfont icon-zan10" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
									<text :style='{"lineHeight":"1.5"}'>{{congyezhelist[4].thumbsupnum}}</text>
								</view>
								<view :style='{"color":"#8fb9e9","padding":"0 20rpx 0 0","display":"inline-block"}'>
									<text class="icon iconfont icon-shoucang10" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
									<text :style='{"lineHeight":"1.5"}'>{{congyezhelist[4].storeupnum}}</text>
								</view>
								<view :style='{"color":"#9d93c8","padding":"0 20rpx 0 0","display":"inline-block"}'>
									<text class="icon iconfont icon-chakan2" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
									<text :style='{"lineHeight":"1.5"}'>{{congyezhelist[4].clicknum}}</text>
								</view>
							</view>
						</view>
						<view v-if="congyezhelist.length > 5" @tap="onDetailTap('congyezhe',congyezhelist[5].id)" class="box box6" :style='{"width":"49%","padding":"0","margin":"0","position":"relative","height":"auto"}'>
							<image :style='{"width":"100%","objectFit":"cover","display":"block","height":"240rpx"}' class="list-item-image" mode="aspectFill" v-if="congyezhelist[5].touxiang.substring(0,4)=='http'" :src="congyezhelist[5].touxiang"></image>
							<image :style='{"width":"100%","objectFit":"cover","display":"block","height":"240rpx"}' class="list-item-image" mode="aspectFill" v-else :src="congyezhelist[5].touxiang?baseUrl+congyezhelist[5].touxiang.split(',')[0]:''"></image>
							<view :style='{"width":"100%","padding":"12rpx","flexWrap":"wrap","background":"linear-gradient(270.00deg, rgb(189, 230, 243),rgb(238, 230, 164) 97.532%)","display":"flex"}'>
								<view :style='{"padding":"0 0px","margin":"0 0 4rpx 0","overflow":"hidden","whiteSpace":"nowrap","color":"#333","width":"100%","lineHeight":"1.5","fontSize":"28rpx","textOverflow":"ellipsis"}' class="title ">{{congyezhelist[5].peiwanxingming}}</view>
								<view :style='{"padding":"0 0px","margin":"0 0 4rpx 0","overflow":"hidden","whiteSpace":"nowrap","color":"#333","width":"100%","lineHeight":"1.5","fontSize":"28rpx","textOverflow":"ellipsis"}' class="title ">工作状态:{{congyezhelist[5].gongzuozhuangtai}}</view>
								<view :style='{"padding":"0 0px","margin":"0 0 4rpx 0","overflow":"hidden","whiteSpace":"nowrap","color":"#333","width":"100%","lineHeight":"1.5","fontSize":"28rpx","textOverflow":"ellipsis"}' class="title ">陪玩收费(元/小时):{{congyezhelist[5].peiwanshoufei}}</view>
								<view :style='{"padding":"4rpx 0px","color":"#fff","borderRadius":"40rpx","textAlign":"center","background":"#8fb9e9","width":"100%","order":"11"}'>
									<text class="icon iconfont icon-shijian21" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
									<text :style='{"lineHeight":"1.5"}'>{{congyezhelist[5].addtime.split(' ')[0].replace(/\-/g,'-')}}</text>
								</view>
								<view :style='{"color":"#a7c839","padding":"0 20rpx 0 0","display":"inline-block"}'>
									<text class="icon iconfont icon-zan10" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
									<text :style='{"lineHeight":"1.5"}'>{{congyezhelist[5].thumbsupnum}}</text>
								</view>
								<view :style='{"color":"#8fb9e9","padding":"0 20rpx 0 0","display":"inline-block"}'>
									<text class="icon iconfont icon-shoucang10" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
									<text :style='{"lineHeight":"1.5"}'>{{congyezhelist[5].storeupnum}}</text>
								</view>
								<view :style='{"color":"#9d93c8","padding":"0 20rpx 0 0","display":"inline-block"}'>
									<text class="icon iconfont icon-chakan2" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
									<text :style='{"lineHeight":"1.5"}'>{{congyezhelist[5].clicknum}}</text>
								</view>
							</view>
						</view>
					</view>
				</view>
			</view>
			<!-- 商品推荐 -->
			
			<!-- 商品列表 -->
			<!-- 商品列表 -->
			<!-- 新闻资讯 -->
			<view class="listBox news" :style='{"padding":"0px","margin":"0px auto","borderRadius":"20rpx","flexWrap":"wrap","background":"none","display":"flex","width":"calc(100% - 48rpx)","position":"relative","height":"auto","order":"9"}'>
				<view class="title" :style='{"padding":"0px","margin":"0 0 40rpx","borderColor":"#23baf7","color":"#8fb9e9","textAlign":"left","background":"url(http://codegen.caihongy.cn/20241123/718dc8bbcb6441929f2293e30cf62f81.png) no-repeat right bottom / 80%","borderWidth":"0 0 0 0px","width":"100%","fontSize":"32rpx","lineHeight":"80rpx","position":"relative","borderStyle":"solid","fontWeight":"600"}'>
					<view :style='{"color":"#B0CB5E","fontSize":"36rpx","fontWeight":"600"}'>通知公告</view>
					<view :style='{"border":"0px solid #1ccb96","padding":"0 0 0 100rpx","margin":"0 auto","textAlign":"center","display":"block","right":"40rpx","top":"0px","borderRadius":"0px","background":"url(http://codegen.caihongy.cn/20241123/d706e58d4e4e4aba948ab1a6232ea8c6.png) no-repeat left center / 80rpx","width":"auto","lineHeight":"80rpx","position":"absolute","zIndex":"999"}' @tap="onPageTap('news')">
					  <text :style='{"color":"#B0CB5E","fontSize":"28rpx","fontWeight":"500"}'>更多</text>
					  <text class="icon iconfont icon-jinru" :style='{"color":"#fff","fontSize":"28rpx","display":"none"}'></text>
					</view>
				</view>
				<!-- 样式3 -->
				<view class="list-box style3" :style='{"padding":"0","margin":"0","color":"#888","flexWrap":"wrap","display":"flex","width":"100%","fontSize":"26rpx","justifyContent":"space-between","height":"auto"}'>
					<view @tap="onNewsDetailTap(item.id)" v-for="(item,index) in news" :key="index" class="list-item" :style='{"margin":"0 0 30rpx","borderRadius":"12rpx","flexWrap":"wrap","background":"none","display":"flex","width":"48%","height":"auto"}'>
						<image v-if="item.picture" :style='{"padding":"8rpx","objectFit":"cover","borderRadius":"200rpx 200rpx 0 0","background":"linear-gradient(153.43deg, rgb(238, 230, 164) 0.429%,rgb(186, 229, 246) 92.448%)","display":"block","width":"100%","height":"360rpx"}' class="list-item-image" mode="aspectFill" :src="baseUrl+item.picture"></image>
						<view class="list-item-body" :style='{"padding":"10rpx","margin":"0","borderColor":"#bae5f6","flexWrap":"wrap","borderWidth":"0 8rpx 8rpx 8rpx","display":"flex","width":"calc(100% - 0px)","borderStyle":"solid","height":"auto","order":"2"}'>
							<view :style='{"padding":"0 0px","margin":"0","overflow":"hidden","whiteSpace":"nowrap","color":"#224366","width":"100%","lineHeight":"48rpx","fontSize":"28rpx","textOverflow":"ellipsis"}' class="list-item-title">{{item.title}}</view>
							<view :style='{"padding":"0 0px","overflow":"hidden","color":"#999","maxHeight":"96rpx","width":"100%","lineHeight":"48rpx","fontSize":"28rpx"}' class="text">{{item.introduction}}</view>
							<view :style='{"margin":"0 0px 0 0","color":"#2dabdd","display":"inline-block","order":"11"}'>
								<text class="icon iconfont icon-shijian21" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
								<text :style='{"lineHeight":"1.5"}'>{{item.addtime.split(' ')[0].replace(/\-/g,'-')}}</text>
							</view>
							<view :style='{"margin":"0 10rpx 0 0","color":"#4bc942","display":"inline-block","order":"10"}'>
								<text class="icon iconfont icon-geren16" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
								<text :style='{"lineHeight":"1.5"}'>{{item.name}}</text>
							</view>
							<view :style='{"color":"#9ea5de","margin":"0 10rpx 0 0","display":"inline-block"}'>
								<text class="icon iconfont icon-zan10" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
								<text :style='{"lineHeight":"1.5"}'>{{item.thumbsupnum}}</text>
							</view>
							<view :style='{"color":"#bc9ad5","margin":"0 10rpx 0 0","display":"inline-block"}'>
								<text class="icon iconfont icon-shoucang10" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
								<text :style='{"lineHeight":"1.5"}'>{{item.storeupnum}}</text>
							</view>
							<view :style='{"color":"#d6a1d6","margin":"0 10rpx 0 0","display":"inline-block"}'>
								<text class="icon iconfont icon-chakan2" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
								<text :style='{"lineHeight":"1.5"}'>{{item.clicknum}}</text>
							</view>
						</view>
					</view>
				</view>
			</view>
			<!-- 新闻资讯 -->
			<view v-if="scrollTop>200" @tap="scrollTopClick" :style='{"boxShadow":"0 8rpx 16rpx rgba(0,0,0,.3)","borderRadius":"50%","textAlign":"center","bottom":"20%","background":"#ff000030","width":"60rpx","lineHeight":"60rpx","position":"fixed","right":"20rpx","height":"60rpx","zIndex":"9999"}'>
				<span class="icon iconfont icon-jiantou07" :style='{"color":"#fff"}'></span>
			</view>
		</view>
	</view>
</template>

<script>
    import menu from '@/utils/menu'
	import '@/assets/css/global-restaurant.css'
	import uniIcons from "@/components/uni-ui/lib/uni-icons/uni-icons.vue"
	export default {
		components: {
			uniIcons
		},
		data() {
			return {
				startX: 0,
				prevNumList4: '',
				numList4: 0,
				timerList4: null,
				flagList4: false,
				navigationActive: {"width":"16rpx","margin":"0 4rpx","borderRadius":"100%","background":"#d6b8ff","height":"16rpx"},
				navigationDefault: {"width":"16rpx","margin":"0 4rpx","borderRadius":"100%","background":"#fff","height":"16rpx"},
				options2: {
					effect: 'flip',
					loop : true
				},
				options3: {
					effect: 'cube',
					loop : true,
					cubeEffect: {
						shadow: true,
						slideShadows: true,
						shadowOffset: 20,
						shadowScale: 0.94,
					}
				},
				rows: 2,
				column: 4,
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
				role : '',
				menuList: [],
				swiperMenuList:[],
				user: {},
				tableName:'',
				menuColor: '#6580a6,#548aff,#ffc431,#ff6161,#4f91ff,#ffbd65,#0fd38c,#52c9e1,#0fd38c,#52c9e1,#0fd38c,#52c9e1'.split(','),
				btnColor: ['#409eff','#67c23a','#909399','#e6a23c','#f56c6c','#356c6c','#351c6c','#f093a9','#a7c23a','#104eff','#10441f','#a21233','#503319'],
				queryList:[
					{
						queryName:"陪玩姓名",
					},
				],
				queryIndex: 0,
				searchForm:{
					congyezhepeiwanxingming:'',
				},
				CustomBar: '0',

				//轮播
				swiperList: [],
				congyezhelist: [],
				news: [],
				scrollTop: 0,
			}
		},
		onPageScroll(e) {
			this.scrollTop = e.scrollTop
		},
		watch: {
		},
		mounted() {
		},
		computed: {
			baseUrl() {
				return this.$base.url;
			},
		},
		async onLoad(){
			this.menuColor = this.menuColor.sort(()=> {
				return (0.5-Math.random());
			});
		},
		async onShow() {
			if (this.timerList4&&this.timerList4!=null) clearInterval(this.timerList4)
			this.swiperMenuList = []
			this.role = uni.getStorageSync("appRole");
			let table = uni.getStorageSync("nowTable");
			let res = await this.$api.session(table);
			this.user = res.data;
			this.tableName = table;
			let menus = menu.list();
			this.menuList = menus;
			this.menuList.forEach((item,key) => {
				if(key==0) {
					item.frontMenu.forEach((item2,key2) => {
						if(item2.child[0].buttons.indexOf("查看")>-1) {
							this.swiperMenuList.push(item2);
						}
					})
				}
			})
			this.btnColor = this.btnColor.sort(()=> {
				return (0.5-Math.random());
			});
			// let res;
			// 轮播图
			let swiperList = []
			res = await this.$api.list('config', {
				page: 1,
				limit: 5
			});
			for (let item of res.data.list) {
				if (item.name.indexOf('picture') >= 0 && item.value && item.value!="" && item.value!=null ) {
					swiperList.push({
						img: item.value,
						title: item.name,
						url: item.url
					});
				}
			}
			if (swiperList) {
				this.swiperList = swiperList;
			}
			
			this.prevNumList4 = this.swiperList.length - 1
			this.timerList4 = setInterval(this.autoPlayList4, 3000)

			// 推荐信息
			this.getRecommendList()
			this.getHomeList()
			this.getNewsList()
		},
		methods: {
			scrollTopClick(){
				uni.pageScrollTo({
					scrollTop: 0
				})
			},
			uGetRect(selector, all) {
				return new Promise(resolve => {
					uni.createSelectorQuery()
					.in(this)
					[all ? 'selectAll' : 'select'](selector)
					.boundingClientRect(rect => {
						if (all && Array.isArray(rect) && rect.length) {
							resolve(rect);
						}
						if (!all && rect) {
							resolve(rect);
						}
					})
					.exec();
				});
			},
			cloneData(data) {
				return JSON.parse(JSON.stringify(data));
			},
			newsTabClick2(index){
				this.newsIndex2 = index
				this.getNewsList()
			},
			async getNewsList(){
				let res;
				let params = {
					page: 1,
					limit: 4,
					sort: 'id',
					order: 'desc',
				}
				// 通知公告
				res = await this.$api.list('news', params)
				this.news = res.data.list
			},
			homeTabClick2(index,name){
				this['home' + name + 'Index2'] = index
				this.getHomeList()
			},
			async getHomeList(){
				let res;
				let params;
			},
			recommendTabClick2(index,name){
				this[name + 'Index2'] = index
				this.getRecommendList()
			},
			async getRecommendList(){
				let res;
				let params;
				// 推荐信息
				params = {
					page: 1,
					limit: 6,
				}
				if(uni.getStorageSync("appUserid")) {
					res = await this.$api.recommend2('congyezhe', params);
				} else {
					res = await this.$api.recommend('congyezhe', params);
				}
				this.congyezhelist = res.data.list
				

			},
			autoPlayList4() {
				this.prevNumList4 = this.numList4
			
				this.numList4++
				if (this.numList4 == this.swiperList.length) this.numList4 = 0
			},
			touchStart(event) {
				this.startX = event.touches[0].clientX
				
				clearInterval(this.timerList4)
				this.flagList4 = true
			},
			touchMove(event) {
				const currentX = event.touches[0].clientX;
				const deltaX = currentX - this.startX;
				
				if (deltaX > 50) {
					// 向右滑动逻辑
					if (this.flagList4) {
						this.flagList4 = false
						
						this.prevNumList4 = this.numList4
						this.numList4++
						if (this.numList4 == this.swiperList.length) this.numList4 = 0
					}
					
				} else if (deltaX < -50) {
					// 向左滑动逻辑
					if (this.flagList4) {
						this.flagList4 = false
						
						this.prevNumList4 = this.numList4
						this.numList4--
						if (this.numList4 < 0) this.numList4 = this.swiperList.length - 1
					}
				}
			},
			touchEnd() {
				this.startX = 0
				this.timerList4 = setInterval(this.autoPlayList4, 3000)
				this.flagList4 = false
			},
			//查询条件切换
			queryChange(e) {
				this.queryIndex=e.detail.value;
				this.searchForm.congyezhepeiwanxingming="";
			},
			//轮播图跳转
			onSwiperTap(e) {
				if(e.url) {
					if (e.url.indexOf('https') != -1) {
						// #ifdef MP-WEIXIN
						uni.navigateTo({
						    url: '../../common/linkOthers/linkOthers?url=' + encodeURIComponent(e.url),
						});
						return false
						// #endif
						window.open(e.url)
					} else {
						this.$utils.jump(e.url)
					}
				}
			},
			// 新闻详情
			onNewsDetailTap(id) {
				this.$utils.jump(`../news-detail/news-detail?id=${id}`)
			},
			// 推荐列表点击详情
			onDetailTap(tableName, id) {
				this.$utils.jump(`../${tableName}/detail?id=${id}`)
			},
			onPageTap(tableName){
				if(this.queryIndex==0) {
					uni.setStorageSync('indexQueryCondition',this.searchForm.congyezhepeiwanxingming);
					this.searchForm.congyezhepeiwanxingming = '';
				}
				uni.navigateTo({
					url: `../${tableName}/list`,
					fail: function(){
						uni.switchTab({
							url: `../${tableName}/list`
						});
					}
				});
				// this.$utils.jump(`../${tableName}/list`)
			},
			onPageTap2(index) {
				let url = '../' + index + '/list'
				if(index=='forum'){
					url = '../forum-index/forum-index'
				}
				if(index=='kefuguanli') {
					url = '../chat/chat'
				}
				uni.setStorageSync("useridTag",0);
				uni.navigateTo({
					url: url,
					fail: function() {
						uni.switchTab({
							url: url
						});
					}
				});
			}
		}
	}
</script>

<style lang="scss" scoped>
	.content {
		min-height: calc(100vh - 44px);
		box-sizing: border-box;
	}
	.list-swiper-4 .animate__animated {
		--animate-delay: 300ms;
	}

	.menu_view {
		border-radius: 20rpx;
		padding: 0;
		margin: 0px auto 0;
		background: none;
		display: flex;
		width: calc(100% - 48rpx);
		flex-wrap: wrap;
		height: auto;
		.menu-item {
			border-radius: 8rpx;
			padding: 12rpx 0;
			margin: 10rpx 0px;
			width: calc(25% - 0px);
			height: auto;
			.iconarr {
				border-radius: 40rpx;
				padding: 0;
				margin: 0px auto;
				color: rgba(255,255,255,1);
				background: none;
				display: block;
				width: 96rpx;
				font-size: 64rpx;
				line-height: 96rpx;
				text-align: center;
				height: 96rpx;
			}
			.text {
				padding: 0;
				margin: 12rpx auto 0;
				color: #224366;
				width: 100%;
				font-size: 26rpx;
				line-height: 28rpx;
				text-align: center;
			}
		}
	}
</style>
