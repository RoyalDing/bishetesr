<template>
<!-- category 1 -->
	<mescroll-uni @init="mescrollInit" :up="upOption" :down="downOption" @down="downCallback" @up="upCallback">
		<view class="content">
			<view :style='{"alignContent":"flex-start","minHeight":"100vh","padding":"0 24rpx 128rpx","borderColor":"#c0c0c0","alignItems":"flex-start","flexWrap":"wrap","background":"#fff","borderWidth":"2rpx 0 0 0","display":"flex","width":"100%","borderStyle":"solid","height":"auto"}'>
				<view class="cu-bar bg-white search" :style='{"width":"calc(100% - 90rpx)","padding":"20rpx 0","background":"none","display":"flex","height":"auto"}'>
					<view :style='{"border":"2rpx solid #b0cb5e","margin":"0 12rpx 0 0","borderRadius":"60rpx","flex":"1","background":"#f8fff7","position":"relative","height":"88rpx"}' class="search-form round">
						<text class="icon iconfont icon-fangdajing07" :style='{"color":"#d6b8ff","left":"0px","textAlign":"center","display":"none","width":"80rpx","fontSize":"40rpx","lineHeight":"80rpx","position":"absolute","right":"0px"}'></text>
						<input placeholder-style="color: #333" :style='{"border":"0","padding":"12rpx 24rpx 12rpx 24rpx","color":"#333","borderRadius":"60rpx","background":"none","width":"100%","lineHeight":"56rpx","fontSize":"28rpx","height":"80rpx"}' v-model="searchForm.title" type="text" placeholder="标题" ></input>
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
					<scroll-view scroll-x="true" class="category-one" :style='{"border":"2rpx solid #b1c387","width":"100%","padding":"24rpx 24rpx 0","whiteSpace":"nowrap","borderRadius":"8rpx 8rpx 0 0 "}'>
						<view :class='categoryName === item.typename ? "active" : ""' class="tab" v-for="(item,index) in categoryList" :key="index" @tap="categoryClick(item.typename)">{{item.typename}}</view>
					</scroll-view>
					<!-- 样式1 -->
					<view class="news-box1" :style='{"padding":"0","margin":"40rpx 0 0 0","color":"#888","flexWrap":"wrap","display":"flex","width":"100%","fontSize":"26rpx","justifyContent":"space-between","height":"auto"}'>
						<view @tap="onDetailTap(product)" v-for="(product,index) in list" :key="index" class="list-item" :style='{"margin":"0 0 30rpx","borderRadius":"12rpx","flexWrap":"wrap","background":"none","display":"flex","width":"48%","height":"auto"}'>
							<view class="list-item-body" :style='{"padding":"10rpx","margin":"0","borderColor":"#bae5f6","flexWrap":"wrap","borderWidth":"0 8rpx 8rpx 8rpx","display":"flex","width":"calc(100% - 0px)","borderStyle":"solid","height":"auto","order":"2"}'>
								<view :style='{"padding":"0 0px","margin":"0","overflow":"hidden","whiteSpace":"nowrap","color":"#224366","width":"100%","lineHeight":"48rpx","fontSize":"28rpx","textOverflow":"ellipsis"}' class="title ">{{product.title}}</view>
								<view :style='{"padding":"0 0px","overflow":"hidden","color":"#999","maxHeight":"96rpx","width":"100%","lineHeight":"48rpx","fontSize":"28rpx"}' class="text ">{{product.introduction}}</view>
								<view :style='{"margin":"0 0px 0 0","color":"#2dabdd","display":"inline-block","order":"11"}'>
									<text class="icon iconfont icon-shijian21" :style='{"margin":"0 0px 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
									<text :style='{"lineHeight":"1.5"}'>{{product.addtime.split(' ')[0].replace(/\-/g,'-')}}</text>
								</view>
								<view :style='{"margin":"0 10rpx 0 0","color":"#4bc942","display":"inline-block","order":"10"}'>
									<text class="icon iconfont icon-geren16" :style='{"margin":"0 0px 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
									<text :style='{"lineHeight":"1.5"}'>{{product.name}}</text>
								</view>
								<view :style='{"color":"#9ea5de","margin":"0 10rpx 0 0","display":"inline-block"}'>
									<text class="icon iconfont icon-zan10" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
									<text :style='{"lineHeight":"1.5"}'>{{product.thumbsupnum}}</text>
								</view>
								<view :style='{"color":"#bc9ad5","margin":"0 10rpx 0 0","display":"inline-block"}'>
									<text class="icon iconfont icon-shoucang10" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
									<text :style='{"lineHeight":"1.5"}'>{{product.storeupnum}}</text>
								</view>
								<view :style='{"color":"#d6a1d6","margin":"0 10rpx 0 0","display":"inline-block"}'>
									<text class="icon iconfont icon-chakan2" :style='{"margin":"0 4rpx 0 0","lineHeight":"1.5","fontSize":"inherit"}'></text>
									<text :style='{"lineHeight":"1.5"}'>{{product.clicknum}}</text>
								</view>
							</view>
							<image :style='{"padding":"8rpx","objectFit":"cover","borderRadius":"200rpx 200rpx 0 0","background":"linear-gradient(153.43deg, rgb(238, 230, 164) 0.429%,rgb(186, 229, 246) 92.448%)","display":"block","width":"100%","height":"360rpx"}' mode="aspectFill" class="listmpic" :src="baseUrl+product.picture"></image>
						</view>
					</view>
			
			
			
			
			


			
			
			
			
				</view>
				<button :style='{"border":"0","color":"rgb(255, 255, 255)","bottom":"128rpx","outline":"none","borderRadius":"100%","left":"40rpx","background":"#EF7061","width":"80rpx","lineHeight":"80rpx","fontSize":"28rpx","position":"absolute","height":"80rpx","zIndex":"999"}' v-if="userid && isAuth('news','新增')" class="add-btn" @click="onAddTap()">新增</button>
				<button :style='{"border":"0","color":"rgb(255, 255, 255)","bottom":"128rpx","outline":"none","borderRadius":"100%","left":"40rpx","background":"#EF7061","width":"80rpx","lineHeight":"80rpx","fontSize":"28rpx","position":"absolute","height":"80rpx","zIndex":"999"}' v-if="!userid && isAuthFront('news','新增')" class="add-btn" @click="onAddTap()">新增</button>
			</view>
		</view>
	</mescroll-uni>
</template>

<script>
	export default {
		data() {
			return {
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
					title: '',
				},
				categoryList:[],
				categoryName :'全部',
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
			let res = {};
			if(this.userid) {
				res = await this.$api.page('newstype', {page:1,limit:100});
			} else {
				res = await this.$api.list('newstype', {page:1,limit:100});
			}
			res.data.list.splice(0,0,{id:0,typename:'全部'})
			this.categoryList = res.data.list;
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
		},
		components: {
		},
		methods: {
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
			categoryClick(categoryName){
				this.categoryName = categoryName;
				this.mescroll.resetUpScroll();
			},
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

				if(this.categoryName!='全部'){
					params.typename = this.categoryName
				}
				if(this.searchForm.title){
					params['title'] = '%' + this.searchForm.title + '%'
				}
				let user = uni.getStorageSync("appUserid")?JSON.parse(uni.getStorageSync('userSession')):{}
                let res = {}
                if(this.userid) {
                    res = await this.$api.page(`news`, params);
                } else {
                    res = await this.$api.list(`news`, params);
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
				this.$utils.jump(`../news-detail/news-detail?id=${item.id}`)
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
							await _this.$api.del('news', JSON.stringify([id]));
							let obj = await _this.$api.list('storeup',{
								page: 1,
								limit: 100,
								tablename: 'news',
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

				if(this.categoryName!='全部'){
					searchForm.typename = this.categoryName
				}
				if(this.searchForm.title){
					searchForm['title'] = '%' + this.searchForm.title + '%'
				}
                let res = {};
                if(this.userid) {
                    res = await this.$api.page(`news`, searchForm);
                } else {
                    res = await this.$api.list(`news`, searchForm);
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
</style>
