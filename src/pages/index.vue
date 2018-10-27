<template>
	<div class="container">
		<div class="index-left">
			<div class="index-left-block">
				<h2>全部产品</h2>
				<template v-for="product in productList">
					<h3>{{ product.title }}</h3>
					<ul>
						<li v-for="item in product.list">
							<a :href="item.url">{{ item.name }}</a>
							<span v-if="item.hot" class="hot">HOT</span>
						</li>
					</ul>
					<div v-if="!product.last" class="hr"></div>
				</template>
			</div>
			<div class="index-left-block lastest-news">
				<h2>最新消息</h2>		
				<ul>
					<li v-for="item in newsList">
						<a :href="item.url">{{ item.title }}</a>
					</li>					
				</ul>
			</div>
		</div>
		<div class="index-right">
			<slide-show :slides="slides" :inv="invTime" @onchange="doSomethingOnSlideChange"></slide-show>
			<div class="index-board-list">
				<div class="index-board-item" v-for="(item, index) in boardList" :class="['index-board-' + index, {'line-last': (index + 1) % 2 === 0}]">
					<div class="index-board-item-inner">
						<h2>{{ item.title }}</h2>
						<p>{{ item.description }}</p>
						<div class="index-board-button">
							<router-link class="button" :to="{ path: 'detail' }">立即购买</router-link>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	import slideShow from '../components/slideShow'
	export default {
		data () {
			return {
				invTime: 3000,
				slides: [
					{
						src: require('../assets/slideShow/pic1.jpg'),
						title: 'xxx1',
						href: ''
					},
					{
						src: require('../assets/slideShow/pic2.jpg'),
						title: 'xxx2',
						href: ''
					},
					{
						src: require('../assets/slideShow/pic3.jpg'),
						title: 'xxx3',
						href: ''
					},
					{
						src: require('../assets/slideShow/pic4.jpg'),
						title: 'xxx4',
						href: ''
					}
				],
				boardList: [
					{
						title: '开放产品',
						description: '开放产品是一款开放产品',
						saleout: false
					},
					{
						title: '品牌营销',
						description: '品牌营销帮助你的产品更好地找到定位',
						saleout: false
					},
					{
						title: '使命必达',
						description: '使命发达快速迭代永远保持最前端的速度',
						saleout: true
					},
					{
						title: '勇攀高峰',
						description: '帮你勇闯高峰，到达事业的顶峰',
						saleout: false
					}
				],
				newsList: [
					{
						title: '数据统计',
						url: 'detail/count'
					},
					{
						title: '数据预测',
						url: 'detail/forecast'
					},
					{
						title: '流量分析',
						url: 'detail/analysis',
						hot: true
					},
					{
						title: '广告发布',
						url: 'detail/publish'
					}
				],
				productList: {
					pc: {
						title: 'PC产品',
						list: [
							{
								name: '数据统计',
								url: 'detail/count'
							},
							{
								name: '数据预测',
								url: 'detail/forecast'
							},
							{
								name: '流量分析',
								url: 'detail/analysis',
								hot: true
							},
							{
								name: '广告发布',
								url: 'detail/publish'
							}
						]
					},
					app: {
						title: '手机应用类',
						last: true,
						list: [
							{
								name: '91助手',
								url: 'http://weixin.com'
							},
							{
								name: '产品助手',
								url: 'http://twitter.com'
							},
							{
								name: '智能地图',
								url: 'http://maps.com'
							},
							{
								name: '团队语音',
								url: 'http://phone.com'
							}
						]
					}
				}
			}
		},
		components: {
			slideShow
		},
		methods: {
			doSomethingOnSlideChange () {
				//console.log('doSomethingOnSlideChange')
			}
		}
	}
</script>

<style scoped>
	.index-left {
		float: left;
		width: 300px;
	}
	.index-right {
		float: left;
		width: 900px;
	}
	.index-left-block {
		margin: 15px;
		background: #fff;
		box-shadow: 0 0 1px #ddd;
	}
	.index-left-block .hr {
		width: 100%;
		height: 1px;
		background: #ddd;
	}
	.index-left-block h2 {
		padding: 10px 15px;
		font-size: 16px;
		color: #fff;
		background: #4fc08d;
	}
	.index-left-block h3 {
		padding: 15px 15px 0;
		font-size: 14px;
		color: #222;
	}
	.index-left-block ul {
		padding: 10px 15px;
	}
	.index-left-block li {
		padding: 5px;
	}
	.index-left-block .hot {
		margin-left: 5px;
		padding: 1px 5px;
		font-size: 10px;
		color: #fff;
		border-radius: 5px;
		background: red;
	}
	.index-board-list {
		overflow: hidden;
	}
	.index-board-item {
		float: left;
		margin: 0 20px 20px 0;
		padding: 20px;
		width: 400px;
		background: #fff;
		box-shadow: 0 0 1px #ddd;
	}
	.line-last {
		margin-right: 0
	}
	.index-board-item-inner {
		padding-left: 120px;
		min-height: 125px;
	}
	.index-board-0 .index-board-item-inner {
		background: url(../assets/images/1.png) no-repeat;
	}
	.index-board-1 .index-board-item-inner {
		background: url(../assets/images/2.png) no-repeat;
	}
	.index-board-2 .index-board-item-inner {
		background: url(../assets/images/3.png) no-repeat;
	}
	.index-board-3 .index-board-item-inner {
		background: url(../assets/images/4.png) no-repeat;
	}
	.index-board-item-inner h2 {
		margin-bottom: 10px;
	}
	.index-board-item-inner p {
		margin-bottom: 10px;
	}
	.index-board-item-inner .index-board-button a {
		display: inline-block;
		width: 100px;
		height: 30px;
		line-height: 30px;
		font-size: 14px;
		color: #fff;
		text-align: center;
		background: #4fc08d;
	}
</style>