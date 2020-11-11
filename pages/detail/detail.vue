<template>
	<view class="news-detail">
		<view class="news-hd">{{title}}</view>
		<view class="news-bd">
			<rich-text :nodes="body"></rich-text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: '',
				body: '',
			}
		},
		onLoad(e) {
			console.log(e)
			uni.request({
				url: 'https://unidemo.dcloud.net.cn/api/news/36kr/' + e.newsId,
				method: 'GET',
				data: {},
				success: (res) => {
					const {title, content} = res.data
					this.title = title
					this.body = content
				}
			})
		},
		methods: {
			
		}
	}
</script>

<style>
.news-detail {
	padding: 60upx 40upx;
}
.news-hd {
	text-align: center;
	font-size: 16px;
	font-weight: 600;
	margin-bottom: 40upx;
}
.news-bd {
	color: #666;
}
</style>
