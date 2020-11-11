<template>
	<view class="content">
		<view class="uni-list-news">
			<view class="uni-list-item"
				  v-for="(item, index) in list"
				  :key="index"
				  @tap="goToDetail"
				  :data-newsid="item.post_id">
				<image :src="item.author_avatar" class="uni-item-img"></image>
				<view class="uni-item-content">
					<view class="uni-item-title">{{item.title}}</view>
					<view class="uni-item-bd">{{item.created_at}}</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list: []
			}
		},
		onLoad() {
			uni.request({
				url: 'https://unidemo.dcloud.net.cn/api/news',
				method:'GET',
				success: res => {
					this.list = res.data || []
					// console.log(res.data)
				},
				fail: err => {
					
				}
			})
		},
		methods: {
			goToDetail(e) {
				console.log(e)
				var newsId = e.currentTarget.dataset.newsid
				uni.navigateTo({
					url: '../detail/detail?newsId=' + newsId
				})
			}
		}
	}
</script>

<style>
.uni-list-news {
	padding: 0upx 20upx;
}
.uni-list-item {
	display: flex;
	justify-content: space-between;
	margin-top: 40upx;
	padding: 20upx 0upx;
	border-bottom: 1px solid #eee;
}
.uni-item-img {
	display: block;
	width: 100upx;
	height: 100upx;
	margin-right: 60upx;
	border-radius: 100%;
}
.uni-item-content {
	flex: 1;
	text-align: left;
	/* overflow: hidden; */
}
.uni-item-title {
	/* overflow: hidden;
	text-overflow: ellipsis;
	white-space: nowrap; */
}
.uni-item-bd {
	color: #aaa;
	margin-top: 10upx;
	font-size: 12px;
}
</style>
