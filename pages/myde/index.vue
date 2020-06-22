<template>
	<view class="center">
		<view style=" width: 90%; height: 25upx; margin: 0upx auto;">
			<image src="../../static/myde/状态栏.png" style="width: 100%; height: 25upx;"></image>
		</view>
		<view class="mag">
			<image src="../../static/myde/消息.png" style="width: 40upx; height: 40upx;"></image>
		</view>
		
		<view class="touxiang">
			<image src="../../static/myde/头像.png" style="width: 100upx; height: 100upx;"></image>
			<view style="margin-left: 30upx;">
				<view class="nicheng">
					<text style="font-size: 40upx; color: #000000;">情殇</text>
				</view>
			<text style="font-size: 20upx; color: #555555;">一级分类生活家</text>
			<image src="../../static/myde/箭头.png" style="width: 15upx; height: 23upx;"></image>	
			</view>
		</view>
		<view class="center_menu">
			<view class="menu_item" v-for="item in menus" :key="item.key">
				
				<text>{{item.name}} </text>
				<text v-if="scores!=0 && item.key==3">{{scores}}</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				scores:0,
				avatarUrl:'../../static/fumou-center-template/header.jpg',
				nickname:'昵称',
				status: [{
						key: 1,
						name: '待发货',
					},
					{
						key: 2,
						name: '待收货',
					},
					{
						key: 3,
						name: '待评价',
					},
					{
						key: 4,
						name: '全部订单',
					}
				],
				menus: [{
						name: '会员中心',
						key: 1,
					},
					{
						name: '我的优惠券',
						key: 2,
					},
					{
						name: '我的礼品卡',
						key: 3,
					},
					{
						name: '我的收藏',
						key: 4,
					},
					{
						name: '在线客服',
						key: 5,
					},
					{
						name: '收货地址',
						key: 6,
					},
					{
						name: '设置',
						key: 7,
					}

				]
			};
		},
		methods: {
			getUserInfo(){
				let that = this;
				uni.login({
				  provider: 'weixin',
				  success: function (loginRes) {
				    console.log(loginRes.authResult);
				    // 获取用户信息
				    uni.getUserInfo({
				      provider: 'weixin',
				      success: function (infoRes) {
						  console.log(infoRes);
				        console.log('用户昵称为：' + infoRes.userInfo.nickName);
						that.avatarUrl = infoRes.userInfo.avatarUrl;
						that.nickname = infoRes.userInfo.nickName;
				      }
				    });
				  }
				});
			}
		},
		computed: {

		},
		onLoad() {
			this.scores = getApp().globalData.totalScores;
		}
	}
</script>

<style lang="scss">
	.touxiang{
		width: 90%;
		display: flex;
		height: 100upx;
		margin: 0upx auto;
		margin-top: 70upx;
		border: 1upx solid #4CD964;
	}
	.mag{
		width: 90%;
		display: flex;
		height: 40upx;
		margin: 0upx auto;
		margin-top: 70upx;
		flex-direction: row-reverse;
	}
	#getUserInfo{
		border-radius: 45upx;
		color: 'skyblue';
		font-size: 24upx;
	}
	
	page {
		height: 100%;
	}

	

	.center {
		height: 100%;

		&_top {
			height: 18%;
			background: url('../../static/fumou-center-template/header.jpg') no-repeat 0% 50%;
			background-size: cover;

			// background: #E6E6E6;
			.mask {
				background: rgba(0, 0, 0, .4);
				height: 100%;
			}
		}

		&_box_bg {
			background: #F9F9F9;
			position: relative;

			.profily {
				position: absolute;
				width: 90%;
				// border:1px solid #F7F7F7;
				margin: 0 auto;
				top: -100upx;
				left: 5%;
				background: #FEFEFE;
				padding: 35upx;
				box-sizing: border-box;
				box-shadow: 0px 2px 5px #EDEDED;
			}
		}
	}

	

	.baiban {
		background: #FEFEFE;
		height: 300upx;
	}

	.center_menu {
		width: 100%;
		display: inline-block;

		.menu_item {
			font-size: 28upx;
			letter-spacing: 1px;
			padding: 14px 5%;
			background: #FEFEFE;
			overflow: hidden;
			box-sizing: border-box;
			display: flex;
			align-items: center;
			position: relative;
			border-bottom: 1px solid #EFEFEF;

			&:hover {
				background: #F6F6F6 !important;
			}

			&::after {
				content: '';
				width: 30upx;
				height: 30upx;
				position: absolute;
				right: 5%;
				background: url('../../static/fumou-center-template/right.png') no-repeat;
				background-size: 100%;
			}

			text:nth-of-type(1) {
				margin-left: 10px;
			}

			image {
				width: 40upx;
				height: 40upx;
			}

			&:nth-of-type(4) {
				margin-top: 10px;
			}
		}
	}
</style>

