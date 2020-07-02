<template>
	<scroll-view>
		<!-- 头部 -->
		<view class="heandereonde">
			<view class="ondhe">
				<image class="imgs" :src="surl" />
				<view class="kporids">
					<view class="asdwdabuny" >
						<button class="sys_btn" @click="appLogin" >{{name}}</button>
					</view>
					<text class="qdtexts">签到送好礼</text>
				</view>
				<view class="ewmawivie">
					<image class="ssdwa" src="http://bpic.588ku.com/element_origin_min_pic/01/37/28/39573c44ad6d806.jpg" />
				</view>
			</view>
			<view class="bottview">
				<view class="adsauq">
					<text class="jfd">积分</text>
					<text class="jfddssw">-</text>
				</view>
				<view class="adsauq">
					<text class="jfd">资产.充值</text>
					<text class="jfddssw">-</text>
				</view>
				<view class="adsauq">
					<text class="jfd">优惠券</text>
					<text class="jfddssw">-</text>
				</view>
				<view class="adsauq">
					<text class="jfd">礼品</text>
					<text class="jfddssw">-</text>
				</view>
			</view>
		</view>
		<!-- 第二部分 -->
		<view class="towhend">
			<view class="dadqwa">
				<view class="mysw">我的订单</view>
				<view class="adwpp">
					<text class="alltext">全部订单</text>
					<van-icon name="arrow" />
				</view>
			</view>
			<van-grid column-num="5">
				<van-grid-item icon="shop-collect-o" text="待付款" />
				<van-grid-item icon="orders-o" text="待发货" />
				<van-grid-item icon="logistics" text="待收货" />
				<van-grid-item icon="records" text="待评价" />
				<van-grid-item icon="after-sale" text="退换货" />
			</van-grid>
		</view>
		<!-- 第三部分 -->
		<view class="treseeview">
			<view class="dadqwa">
				<view class="mysw">充值有礼</view>
				<view class="adwpp">
					<text class="alltext">充值中心</text>
					<van-icon name="arrow" />
				</view>
			</view>
			<view class="trenbovue">
				<text class="monpri">￥2000</text>
				<text class="givepric">送价值89.90的赠品</text>
			</view>
		</view>
		<!-- 第四部分 -->
		<view class="footer">
			<van-grid>
				<van-grid-item icon="vip-card" text="会员中心" />
				<van-grid-item icon="video" text="直播间" />
				<van-grid-item icon="shop" text="天天新鲜屋" />
				<van-grid-item icon="invition" text="卡卷中心" />
			</van-grid>
			<van-grid>
				<van-grid-item icon="gold-coin" text="企业购" />
				<van-grid-item icon="service" text="在线客服" />
				<van-grid-item icon="question" text="我的问答" />
			</van-grid>
		</view>
		<!-- denglu -->
		
	</scroll-view>

</template>

<script>
	const app = getApp()
	export default {
		data() {
			return {
				name:'授权登录',
				surl:'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1593495206256&di=39c5b99b6b9a3b472a4c65c706f54ac5&imgtype=0&src=http%3A%2F%2Fhbimg.b0.upaiyun.com%2F22e583181c5cd22cccb03c87d8ed16f669405e23121b5-W1F0pp_fw658',
				asdw:''
			}
		},
		methods: {
			 appLogin: function() {
				 let that = this
			                uni.getProvider({
			                    service: 'oauth',
			                    success: function(res) {
			                        console.log(res.provider);
			                        //支持微信、qq和微博等
			                        if (~res.provider.indexOf('weixin')) {
			                            uni.login({
			                                provider: 'weixin',
			                                success: function(loginRes) {
			                                    console.log('-------获取openid(unionid)-----');
			                                    console.log(JSON.stringify(loginRes));
			                                    // 获取用户信息
			                                    uni.getUserInfo({
			                                        provider: 'weixin',
			                                        success: function(infoRes) {
														// let that = this
			                                            console.log('-------获取微信用户所有-----');
			                                            console.log(JSON.stringify(infoRes.userInfo));
														let names = infoRes.userInfo.nickName
														that.name = names
														let url = infoRes.userInfo.avatarUrl
														that.surl = url
														// this.asdw = JSON.stringify(infoRes.userInfo)
														console.log(that.name,that.surl,names,"123+-+-+-+-")
			                                        }
			                                    });
			                                }
			                            });
			                        }
			                    }
			                });
			            },
						 onLoad(options) {
						            console.log(options);
						        },
			        }
		
		
	}
</script>

<style scoped>
	.heandereonde {
		width: 96%;
		height: 191px;
		margin-left: 2%;
		background-color: #F0F0EE;
		margin-top: 5px;
		border-radius: 10px;
	}

	.imgs {
		width: 60px;
		height: 60px;
		border-radius: 36px;
		margin-left: 13px;
		margin-top: 15px;

	}

	.ondhe {
		display: flex;
		flex-direction: row;
		width: 100%;
		height: 70%;
	}

	.ssdwa {
		width: 30px;
		height: 30px;
		margin-left: 30px;
		margin-top: 5px;

	}

	.kporids {
		margin-left: 10px;
		margin-top: 15px;
		display: flex;
		flex-direction: column;
	}

	.sys_btn {
		font-size: 14px;
		font-weight: 700;
		width: 95px;
		height: 35px;
		border: none;
	}
	.qdtexts {
		display: block;
		width: 91px;
		height: 20px;
		background-color: #FF8700;
		font-size: 14px;
		text-align: center;
		border-radius: 8px;
		color: #ffff;
		margin-top: 5px;

	}

	.ewmawivie {
		width: 73px;
		height: 42px;
		margin-left: 146px;
		border-top-left-radius: 38px;
		background-color: #C2C2C2;
		border-bottom-left-radius: 38px;
		margin-top: 15px;
	}

	.bottview {
		display: flex;
		flex-direction: row;
		justify-content: space-evenly;
	}

	.adsauq {
		display: flex;
		flex-direction: column;
	}

	.jfd {
		display: block;
		font-size: 14px;
		width: 80px;
		text-align: center;
	}

	.jfddssw {
		display: block;
		width: 80px;
		text-align: center;
	}

	.dadqwa {
		display: flex;
		flex-direction: row;
		padding-top: 20px;
		/* justify-content: space-between; */
		margin-bottom: 26px;

	}

	.towhend {
		width: 96%;
		height: 160px;
		margin-left: 2%;
		background-color: #FCFCFC;
		border: 1px solid #C0C0C0;
		border-radius: 10px;
		margin-top: 15px;
	}

	.adwpp {
		margin-left: 257px;
		display: flex;
		flex-direction: row;
		font-size: 12px;
		font-weight: 700;
	}

	.alltext {
		display: block;
	}

	.mysw {
		margin-left: 15px;
	}

	.treseeview {
		display: flex;
		flex-direction: column;
		width: 96%;
		height: 210px;
		margin-left: 2%;
		background-color: #FCFCFC;
		border: 1px solid #C0C0C0;
		border-radius: 10px;
		margin-top: 15px;
	}

	.trenbovue {
		display: flex;
		flex-direction: column;
		width: 270px;
		height: 128px;
		background-color: #F3F3F3;
		margin-left: 10px;
		border-top-left-radius: 10px;
		border-top-right-radius: 10px;
	}

	.monpri {
		font-size: 40px;
		display: block;
		font-weight: 700;
		margin-top: 25px;
	}

	.givepric {
		display: block;
		font-size: 13px;
		color: #F47E1F;
		margin-left: 18px;
	}

	.footer {
		margin-top: 16px;
	}

	.header {
		margin: 90rpx 0 90rpx 50rpx;
		border-bottom: 1px solid #ccc;
		text-align: center;
		width: 650rpx;
		height: 300rpx;
		line-height: 450rpx;
	}

	.header image {
		width: 200rpx;
		height: 200rpx;
	}

	.content {
		margin-left: 50rpx;
		margin-bottom: 90rpx;
	}

	.content text {
		display: block;
		color: #9d9d9d;
		margin-top: 40rpx;
	}

	.bottom {
		border-radius: 80rpx;
		margin: 70rpx 50rpx;
		font-size: 35rpx;
	}
</style>
