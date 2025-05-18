<template>
<!-- category 1 -->
	<mescroll-uni @init="mescrollInit" :up="upOption" :down="downOption" @down="downCallback" @up="upCallback">
		<view class="content">
			<view :style='{"alignContent":"flex-start","minHeight":"100vh","padding":"0 24rpx 128rpx","borderColor":"#c0c0c0","alignItems":"flex-start","flexWrap":"wrap","background":"#fff","borderWidth":"2rpx 0 0 0","display":"flex","width":"100%","borderStyle":"solid","height":"auto"}'>
				<view class="cu-bar bg-white search" :style='{"width":"calc(100% - 90rpx)","padding":"20rpx 0","background":"none","display":"flex","height":"auto"}'>
					<view :style='{"border":"2rpx solid #b0cb5e","margin":"0 12rpx 0 0","borderRadius":"60rpx","flex":"1","background":"#f8fff7","position":"relative","height":"88rpx"}' class="search-form round">
						<text class="icon iconfont icon-fangdajing07" :style='{"color":"#d6b8ff","left":"0px","textAlign":"center","display":"none","width":"80rpx","fontSize":"40rpx","lineHeight":"80rpx","position":"absolute","right":"0px"}'></text>
						<input placeholder-style="color: #333" :style='{"border":"0","padding":"12rpx 24rpx 12rpx 24rpx","color":"#333","borderRadius":"60rpx","background":"none","width":"100%","lineHeight":"56rpx","fontSize":"28rpx","height":"80rpx"}' v-model="searchForm.peiwanxingming" type="text" placeholder="陪玩姓名" ></input>
					</view>
					<button :style='{"border":"0","padding":"0px","margin":"0","color":"#fff","borderRadius":"60rpx","background":"linear-gradient(30deg, rgba(238,230,164,1) 0%, rgba(181,205,99,1) 100%)","width":"136rpx","lineHeight":"80rpx","fontSize":"28rpx","height":"80rpx"}' @tap="search" class="cu-btn shadow-blur round">搜索</button>
				</view>
			

				<view :style='{"padding":"0px","margin":"20rpx auto 40rpx","color":"#999","flexWrap":"wrap","background":"none","display":"flex","width":"100%","justifyContent":"center","zIndex":"99"}'>
					<view @click="sortClick('clicknum')" :style='{"border":"2rpx solid #ddd","padding":"0 20rpx","margin":"0 20rpx 0 0","outline":"0","borderRadius":"0px","background":"rgba(255,255,255,.3)","display":"flex","height":"48rpx"}'>
						<text :style='{"margin":"0 4rpx 0 0","lineHeight":"48rpx","fontSize":"inherit","color":"inherit"}'>点击量</text>
						<text v-if="listSort!='clicknum'" class="icon iconfont icon-liulan04" :style='{"margin":"0 4rpx 0 0","lineHeight":"48rpx","fontSize":"inherit","color":"inherit"}'></text>
						<text v-else-if="listSort=='clicknum'&&listOrder=='asc'" class="icon iconfont icon-jiantou23" :style='{"margin":"0 4rpx 0 0","lineHeight":"48rpx","fontSize":"inherit","color":"inherit"}'></text>
						<text v-else-if="listSort=='clicknum'&&listOrder=='desc'" class="icon iconfont icon-jiantou24" :style='{"margin":"0 4rpx 0 0","lineHeight":"48rpx","fontSize":"inherit","color":"inherit"}'></text>
					</view>
					<view @click="sortClick('addtime')" :style='{"border":"2rpx solid #ddd","padding":"0 20rpx","margin":"0 20rpx 0 0","outline":"0","borderRadius":"0px","background":"rgba(255,255,255,.3)","display":"flex","height":"48rpx"}'>
						<text :style='{"margin":"0 4rpx 0 0","lineHeight":"48rpx","fontSize":"inherit","color":"inherit"}'>按日期</text>
						<text v-if="listSort!='addtime'" class="icon iconfont icon-shijian21" :style='{"margin":"0 4rpx 0 0","lineHeight":"48rpx","fontSize":"inherit","color":"inherit"}'></text>
						<text v-else-if="listSort=='addtime'&&listOrder=='asc'" class="icon iconfont icon-jiantou23" :style='{"margin":"0 4rpx 0 0","lineHeight":"48rpx","fontSize":"inherit","color":"inherit"}'></text>
						<text v-else-if="listSort=='addtime'&&listOrder=='desc'" class="icon iconfont icon-jiantou24" :style='{"margin":"0 4rpx 0 0","lineHeight":"48rpx","fontSize":"inherit","color":"inherit"}'></text>
					</view>
				</view>
				<view :style='{"alignContent":"flex-start","alignItems":"flex-start","flexWrap":"wrap","background":"none","display":"flex","width":"100%","height":"auto"}'>
					<!-- 样式2 -->
					<view class="list" :style='{"width":"100%","padding":"20rpx 20rpx 2rpx","margin":"0px 0 0","background":"linear-gradient(135.00deg, rgb(238, 230, 164) 0.464%,rgb(215, 237, 239) 100%)","height":"auto"}'>
						<view @tap="onDetailTap(product)" class="listm flex flex-between" :style='{"padding":"12rpx","margin":"0 0 40rpx","backgroundColor":"#fff","color":"#999","flexWrap":"wrap","display":"flex","width":"100%","fontSize":"28rpx","height":"auto"}' v-for="(product,index) in list" :key="index">
							<image :style='{"width":"200rpx","objectFit":"cover","display":"block","height":"240rpx"}' mode="aspectFill" class="listmpic" v-if="preHttp(product.touxiang)" :src="product.touxiang.split(',')[0]"></image>
							<image :style='{"width":"200rpx","objectFit":"cover","display":"block","height":"240rpx"}' mode="aspectFill" class="listmpic" v-else :src="product.touxiang?baseUrl+product.touxiang.split(',')[0]:''"></image>

							<view class="listmr" :style='{"alignContent":"center","padding":"0 0 0 20rpx","margin":"0","alignItems":"center","flexWrap":"wrap","display":"flex","width":"calc(100% - 200rpx)","height":"auto"}'>
								<view class="col3 f30 elip mb15" :style='{"padding":"0","margin":"0","overflow":"hidden","whiteSpace":"nowrap","color":"#224366","width":"100%","lineHeight":"48rpx","fontSize":"28rpx","textOverflow":"ellipsis"}'>{{product.peiwanxingming}}</view>
								<view class="col3 f30 elip mb15" :style='{"padding":"0","margin":"0","overflow":"hidden","whiteSpace":"nowrap","color":"#224366","width":"100%","lineHeight":"48rpx","fontSize":"28rpx","textOverflow":"ellipsis"}'>工作状态:{{product.gongzuozhuangtai}}</view>
								<view class="col3 f30 elip mb15" :style='{"padding":"0","margin":"0","overflow":"hidden","whiteSpace":"nowrap","color":"#224366","width":"100%","lineHeight":"48rpx","fontSize":"28rpx","textOverflow":"ellipsis"}'>陪玩收费(元/小时):{{product.peiwanshoufei}}</view>
								<view :style='{"width":"45%","padding":"0 0px","fontSize":"26rpx","color":"#B2CD63","textAlign":"right","display":"inline-block"}'>
									<text class="icon iconfont icon-shijian21" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
									<text :style='{"lineHeight":"1.5"}'>{{product.addtime.split(' ')[0].replace(/\-/g,'-')}}</text>
								</view>
								<view :style='{"color":"#a7c839","padding":"10rpx 10rpx 0 0","display":"inline-block"}'>
									<text class="icon iconfont icon-zan10" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
									<text :style='{"lineHeight":"1.5"}'>{{product.thumbsupnum}}</text>
								</view>
								<view :style='{"color":"#8fb9e9","padding":"10rpx 10rpx 0 0","display":"inline-block"}'>
									<text class="icon iconfont icon-shoucang10" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
									<text :style='{"lineHeight":"1.5"}'>{{product.storeupnum}}</text>
								</view>
								<view :style='{"color":"#9d93c8","padding":"10rpx 10rpx 0 0","display":"inline-block"}'>
									<text class="icon iconfont icon-chakan2" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
									<text :style='{"lineHeight":"1.5"}'>{{product.clicknum}}</text>
								</view>
							</view>
							<!-- #ifdef MP-WEIXIN -->
							<view :style='{"width":"100%","padding":"8rpx 20rpx","margin":"20rpx 0 0 0","justifyContent":"space-between","display":"flex","height":"auto"}'>
								<view :style='{"border":"2rpx solid #174add","padding":"10rpx","background":"#d3e5ff","display":"flex"}' v-if="(userid && isAuth('congyezhe','修改')) || (!userid && isAuthFront('congyezhe','修改'))" @tap.stop.proevent="onUpdate" :data-row="product">
									<text :style='{"margin":"0 8rpx 0 0","fontSize":"28rpx","lineHeight":"1","color":"#174add","display":"inline-block"}' class="cuIcon-edit"></text>
									<text :style='{"fontSize":"28rpx","lineHeight":"1","color":"#174add","display":"inline-block"}'>修改</text>
								</view>
								<view :style='{"border":"2rpx solid #9a9a9a","padding":"10rpx","background":"#ecebeb","display":"flex"}' v-if="(userid && isAuth('congyezhe','删除')) || (!userid && isAuthFront('congyezhe','删除'))" @tap.stop.proevent="onDelete" :data-row="product">
									<text :style='{"margin":"0 8rpx 0 0","fontSize":"28rpx","lineHeight":"1","color":"#666","display":"inline-block"}' class="cuIcon-delete"></text>
									<text :style='{"fontSize":"28rpx","lineHeight":"1","color":"#666","display":"inline-block"}'>删除</text>
								</view>
							</view>
							<!-- #endif -->
							<!-- #ifndef MP-WEIXIN -->
							<view :style='{"width":"100%","padding":"8rpx 20rpx","margin":"20rpx 0 0 0","justifyContent":"space-between","display":"flex","height":"auto"}'>
								<view :style='{"border":"2rpx solid #174add","padding":"10rpx","background":"#d3e5ff","display":"flex"}' v-if="(userid && isAuth('congyezhe','修改')) || (!userid && isAuthFront('congyezhe','修改'))" @tap.stop.proevent="onUpdateTap(product)">
									<text :style='{"margin":"0 8rpx 0 0","fontSize":"28rpx","lineHeight":"1","color":"#174add","display":"inline-block"}' class="cuIcon-edit"></text>
									<text :style='{"fontSize":"28rpx","lineHeight":"1","color":"#174add","display":"inline-block"}'>修改</text>
								</view>
								<view :style='{"border":"2rpx solid #9a9a9a","padding":"10rpx","background":"#ecebeb","display":"flex"}' v-if="(userid && isAuth('congyezhe','删除')) || (!userid && isAuthFront('congyezhe','删除'))" @tap.stop.proevent="onDeleteTap(product.id)">
									<text :style='{"margin":"0 8rpx 0 0","fontSize":"28rpx","lineHeight":"1","color":"#666","display":"inline-block"}' class="cuIcon-delete"></text>
									<text :style='{"fontSize":"28rpx","lineHeight":"1","color":"#666","display":"inline-block"}'>删除</text>
								</view>
							</view>
							<!-- #endif -->
						</view>
					</view>
			
			
			


			
			
			
			
				</view>
				<button :style='{"border":"0","boxShadow":"0 2rpx 12rpx #00000030","color":"#fff","right":"10rpx","outline":"none","borderRadius":"100%","top":"20rpx","background":"#ffaa33","width":"80rpx","lineHeight":"80rpx","fontSize":"28rpx","position":"absolute","height":"80rpx","zIndex":"999"}' class="add-btn" @click="screenBoxShow=true">筛</button>
				<button :style='{"border":"0","color":"rgb(255, 255, 255)","bottom":"128rpx","outline":"none","borderRadius":"100%","left":"40rpx","background":"#EF7061","width":"80rpx","lineHeight":"80rpx","fontSize":"28rpx","position":"absolute","height":"80rpx","zIndex":"999"}' v-if="userid && isAuth('congyezhe','新增')" class="add-btn" @click="onAddTap()">新增</button>
				<button :style='{"border":"0","color":"rgb(255, 255, 255)","bottom":"128rpx","outline":"none","borderRadius":"100%","left":"40rpx","background":"#EF7061","width":"80rpx","lineHeight":"80rpx","fontSize":"28rpx","position":"absolute","height":"80rpx","zIndex":"999"}' v-if="!userid && isAuthFront('congyezhe','新增')" class="add-btn" @click="onAddTap()">新增</button>
				<view :style='{"top":"0","left":"0","background":"rgba(0, 0, 0, .3)","width":"100%","position":"absolute","height":"100%","zIndex":"665"}' v-if="screenBoxShow" @click="screenBoxShow=false"></view>
				<view class="screenBox" :class="screenBoxShow?'screenBoxActive':''">
					<view :style='{"width":"100%","padding":"20rpx 0 20rpx 0"}'>
						<view :style='{"width":"100%","padding":"0 0 20rpx 20rpx","fontSize":"24rpx"}'>性别</view>
						<view :style='{"width":"100%","flexWrap":"wrap","justifyContent":"space-around","display":"flex"}'>
							<view @click="xingbieChange(item)" v-for="(item,index) in xingbieOptions" :key="index" class="screenTab" :class="searchForm.xingbie==item?'screenTabActive':''">{{item}}</view>
						</view>
					</view>
					<view :style='{"width":"100%","padding":"20rpx 0 20rpx 0"}'>
						<view :style='{"width":"100%","padding":"0 0 20rpx 20rpx","fontSize":"24rpx"}'>工作状态</view>
						<view :style='{"width":"100%","flexWrap":"wrap","justifyContent":"space-around","display":"flex"}'>
							<view @click="gongzuozhuangtaiChange(item)" v-for="(item,index) in gongzuozhuangtaiOptions" :key="index" class="screenTab" :class="searchForm.gongzuozhuangtai==item?'screenTabActive':''">{{item}}</view>
						</view>
					</view>
					<view :style='{"width":"100%"}'>
						<view :style='{"width":"100%","padding":"0 0 20rpx 20rpx","fontSize":"28rpx"}'>陪玩收费(元/小时)区间</view>
						<view :style='{"width":"100%","alignItems":"center","flexWrap":"wrap","justifyContent":"center","display":"flex"}'>
							<input :style='{"border":"0","borderRadius":"0px","textAlign":"center","background":"#f3f5f9","width":"47%","lineHeight":"72rpx","fontSize":"24rpx","height":"72rpx"}' v-model="searchForm.peiwanshoufeistart" placeholder="请输入开始陪玩收费(元/小时)">
							<view :style='{"padding":"0 4rpx","fontSize":"20rpx"}'>-</view>
							<input :style='{"border":"0","borderRadius":"0px","textAlign":"center","background":"#f3f5f9","width":"47%","lineHeight":"72rpx","fontSize":"24rpx","height":"72rpx"}' v-model="searchForm.peiwanshoufeiend" placeholder="请输入结束陪玩收费(元/小时)">
						</view>
					</view>
					<view :style='{"width":"100%","padding":"20rpx 0 20rpx 0","alignItems":"center","justifyContent":"space-around","display":"flex"}'>
						<view :style='{"width":"auto","padding":"0 20rpx 0 20rpx","fontSize":"24rpx","whiteSpace":"nowrap"}'>擅长游戏</view>
						<input :style='{"border":"0","padding":"0 20rpx 0 20rpx","margin":"0 16rpx 0 0","borderRadius":"8rpx","background":"#f3f5f9","flex":"1","width":"75%","fontSize":"28rpx","height":"68rpx"}' placeholder="请输入擅长游戏" v-model="searchForm.youxileibie">
					</view>
					<view :style='{"width":"100%","padding":"40rpx 0 0","alignItems":"center","justifyContent":"space-around","display":"flex"}'>
						<div :style='{"color":"#888","borderRadius":"8rpx","textAlign":"center","background":"#ededed","width":"30%","lineHeight":"68rpx","height":"68rpx"}' @click="screenReset">重置</div>
						<div :style='{"color":"#fff","borderRadius":"8rpx","textAlign":"center","background":"#03b882","width":"30%","lineHeight":"68rpx","height":"68rpx"}' @click="search">搜索</div>
					</view>
				</view>
			</view>
		</view>
	</mescroll-uni>
</template>

<script>
	export default {
		data() {
			return {
				xingbieOptions:[],
				gongzuozhuangtaiOptions:[],
				btnColor: ['#409eff','#67c23a','#909399','#e6a23c','#f56c6c','#356c6c','#351c6c','#f093a9','#a7c23a','#104eff','#10441f','#a21233','#503319'],
				clicknumColor: ['#409eff','#67c23a','#909399','#e6a23c','#f56c6c','#356c6c','#351c6c','#f093a9','#a7c23a','#104eff','#10441f','#a21233','#503319'],
				list: [],
				lists: [],
                userid: '',
				mescroll: null, //mescroll实例对象
				downOption: {
					auto: false //是否在初始化后,自动执行下拉回调callback; 默认true
				},
				upOption: {
					noMoreSize: 5, //如果列表已无数据,可设置列表的总数量要大于半页才显示无更多数据;避免列表数据过少(比如只有一条数据),显示无更多数据会不好看; 默认5
					textNoMore: '~ 没有更多了 ~',
				},
				hasNext: true,
				searchForm:{
					peiwanxingming: '',
					xingbie: '',
					gongzuozhuangtai: '',
					peiwanshoufeistart: '',
					peiwanshoufeiend: '',
					youxileibie: '',
				},
				CustomBar: '0',
				listSort: 'id',
				listOrder: 'desc',
				screenBoxShow: false,
			};
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
		async onShow() {
			this.btnColor = this.btnColor.sort(()=> {
				return (0.5-Math.random());
			});
			this.clicknumColor = this.clicknumColor.sort(()=> {
				return (0.5-Math.random());
			});
			this.hasNext = true
			// 重新加载数据
			if (this.mescroll) this.mescroll.resetUpScroll()
		},
		async onLoad(options) {
            if(options.userid) {
                this.userid=options.userid;
            } else {
                this.userid = "";
            }
			this.hasNext = true
			// 重新加载数据
			// if (this.mescroll) this.mescroll.resetUpScroll()
			let res = {};
			this.xingbieOptions = '男,女'.split(',')
			this.gongzuozhuangtaiOptions = '未上线,已上线'.split(',')
		},
		components: {
		},
		methods: {
			xingbieChange(e){
				this.searchForm.xingbie = e
				this.$forceUpdate()
			},
			gongzuozhuangtaiChange(e){
				this.searchForm.gongzuozhuangtai = e
				this.$forceUpdate()
			},
			screenReset(){
				this.searchForm = {}
				this.search()
				this.$forceUpdate()
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
			sortClick(type){
				if(this.listSort==type){
					if(this.listOrder == 'desc'){
						this.listOrder = 'asc'
					}else{
						this.listOrder = 'desc'
					}
				}else{
					this.listSort = type
					this.listOrder = 'desc'
				}
				this.search()
			},
            priceChange(price) {
                return Number(price).toFixed(2);
            },
            preHttp(str) {
                return str && str.substr(0,4)=='http';
            },
			//类别搜索
			// mescroll组件初始化的回调,可获取到mescroll对象
			mescrollInit(mescroll) {
				this.mescroll = mescroll;
			},
			/*下拉刷新的回调 */
			downCallback(mescroll) {
				this.hasNext = true
				// 重置分页参数页数为1
				mescroll.resetUpScroll()
			},
			/*上拉加载的回调: mescroll携带page的参数, 其中num:当前页 从1开始, size:每页数据条数,默认10 */
			async upCallback(mescroll) {
				let params = {
					page: mescroll.num,
					limit: mescroll.size,
				}
				params['sort'] = this.listSort;
				params['order'] = this.listOrder;

				if(this.searchForm.peiwanxingming){
					params['peiwanxingming'] = '%' + this.searchForm.peiwanxingming + '%'
				}
				if(this.searchForm.xingbie){
					params['xingbie'] = '%' + this.searchForm.xingbie + '%'
				}
				if(this.searchForm.gongzuozhuangtai){
					params['gongzuozhuangtai'] = '%' + this.searchForm.gongzuozhuangtai + '%'
				}
				if(this.searchForm.peiwanshoufei){
					params['peiwanshoufei'] = '%' + this.searchForm.peiwanshoufei + '%'
				}
				if(this.searchForm.youxileibie){
					params['youxileibie'] = '%' + this.searchForm.youxileibie + '%'
				}
				let indexQueryCondition = uni.getStorageSync('indexQueryCondition');
				if(indexQueryCondition) {
					params['peiwanxingming'] = '%' + indexQueryCondition + '%';
					uni.removeStorageSync('indexQueryCondition');
				}
				let user = uni.getStorageSync("appUserid")?JSON.parse(uni.getStorageSync('userSession')):{}
                let res = {}
                if(this.userid) {
                    res = await this.$api.page(`congyezhe`, params);
                } else {
                    res = await this.$api.list(`congyezhe`, params);
                }

				// 如果是第一页数据置空
				if (mescroll.num == 1) this.list = [];
				this.list = this.list.concat(res.data.list);
				this.$forceUpdate()
				
				let length = Math.ceil(this.list.length/6)
				let arr = [];
				for (let i = 0; i<length; i++){
					arr[i] = this.list.slice(i*6, (i+1)*6)
				}
				this.lists = arr
				if (res.data.list.length == 0) this.hasNext = false;
				mescroll.endSuccess(mescroll.size, this.hasNext);
			},
			// 详情
			onDetailTap(item) {
                uni.setStorageSync("useridTag",this.userid);
				this.$utils.jump(`./detail?id=${item.id}&userid=`+this.userid)
			},
			onUpdate(e){
				this.onUpdateTap(e.currentTarget.dataset.row)
			},
			// 修改
			onUpdateTap(row){
                uni.setStorageSync("useridTag",this.userid);
				this.$utils.jump(`./add-or-update?id=${row.id}`)
			},
			// 添加
			onAddTap(){
                uni.setStorageSync("useridTag",this.userid);
				this.$utils.jump(`./add-or-update`)
			},
			onDelete(e){
				this.onDeleteTap(e.currentTarget.dataset.row.id)
			},
			onDeleteTap(id){
				var _this = this;
				uni.showModal({
					title: '提示',
					content: '是否确认删除',
					success: async function(res) {
						if (res.confirm) {
							await _this.$api.del('congyezhe', JSON.stringify([id]));
							let obj = await _this.$api.list('storeup',{
								page: 1,
								limit: 100,
								tablename: 'congyezhe',
								refid: id,
							})
							if(obj.data.list.length){
								let arr = []
								for(let x in obj.data.list){
									arr.push(obj.data.list[x].id)
								}
								await _this.$api.del('storeup',JSON.stringify(arr))
							}
							_this.$utils.msg('删除成功');
							_this.hasNext = true
							// 重置分页参数页数为1
							_this.search()
						}
					}
				});
			},
			// 搜索
			async search(){
				this.mescroll.num = 1
				let searchForm = {
					page: this.mescroll.num,
					limit: this.mescroll.size,
				}
				searchForm['sort'] = this.listSort;
				searchForm['order'] = this.listOrder;

				if(this.searchForm.peiwanxingming){
					searchForm['peiwanxingming'] = '%' + this.searchForm.peiwanxingming + '%'
				}
				if(this.searchForm.xingbie){
					searchForm['xingbie'] = '%' + this.searchForm.xingbie + '%'
				}
				if(this.searchForm.gongzuozhuangtai){
					searchForm['gongzuozhuangtai'] = '%' + this.searchForm.gongzuozhuangtai + '%'
				}
				if(this.searchForm.peiwanshoufeistart){
					searchForm['peiwanshoufeistart'] = this.searchForm.peiwanshoufeistart
				}
				if(this.searchForm.peiwanshoufeiend){
					searchForm['peiwanshoufeiend'] = this.searchForm.peiwanshoufeiend
				}
				if(this.searchForm.youxileibie){
					searchForm['youxileibie'] = '%' + this.searchForm.youxileibie + '%'
				}
                let res = {};
                if(this.userid) {
                    res = await this.$api.page(`congyezhe`, searchForm);
                } else {
                    res = await this.$api.list(`congyezhe`, searchForm);
                }
				// 如果是第一页数据置空
				if (this.mescroll.num == 1) this.list = [];
				this.list = this.list.concat(res.data.list);
				
				let length = Math.ceil(this.list.length/6)
				let arr = [];
				for (let i = 0; i<length; i++){
					arr[i] = this.list.slice(i*6, (i+1)*6)
				}
				this.lists = arr
				if (res.data.list.length == 0) this.hasNext = false;
				this.mescroll.endSuccess(this.mescroll.size, this.hasNext);
				this.screenBoxShow = false
			}
		}
	};
</script>

<style lang="scss" scoped>
	.content {
		min-height: calc(100vh - 44px);
		box-sizing: border-box;
	}
	.category-one .tab {
		cursor: pointer;
		padding: 0;
		margin: 0 40rpx 0 0;
		color: #333;
		background: #fff;
		display: inline-block;
		width: auto;
		font-size: 30rpx;
		border-color: #fff;
		border-width: 0 0 0px;
		line-height: 76rpx;
		border-style: solid;
	}
	
	.category-one .tab.active {
		cursor: pointer;
		padding: 0 20rpx;
		margin: 0 40rpx 0 0;
		color: #fff;
		display: inline-block;
		font-size: 30rpx;
		border-color: #d6b8ff;
		line-height: 80rpx;
		background: url(http://codegen.caihongy.cn/20241125/dae1bf429ee24b4699a3f86a5545375f.png) no-repeat center top / 100% 100%;
		width: auto;
		border-width: 0 0 0px;
		border-style: solid;
		text-align: center;
		min-width: 150rpx;
	}
	.screenBox {
		padding: 120rpx 0 20rpx 0;
		transform: translate3d(100%, 0, 0);
		z-index: 6666;
		top: 0;
		background: #fff;
		width: 90%;
		position: fixed;
		right: 0;
		transition: transform .3s;
		height: 100%;
		.screenTab {
			border-radius: 8rpx;
			margin: 10rpx 0 10rpx 0;
			background: #f3f5f9;
			width: calc(100% / 3 - 24rpx);
			line-height: 64rpx;
			text-align: center;
		}
		.screenTabActive {
			border-radius: 8rpx;
			margin: 10rpx 0 10rpx 0;
			color: #fff;
			background: #03b882;
			width: calc(100% / 3 - 20rpx);
			line-height: 64rpx;
			text-align: center;
		}
	}
	.screenBoxActive {
		transform: translate3d(0, 0, 0);
	}
</style>
