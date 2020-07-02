<template>
	<scroll-view>
		<view>
			新鲜水果
		</view>
		<view class="centertxte">
			<van-tabs :active="active "  color="red"   animated>
			  <van-tab :title='item.name' v-for="(item,index) in topview" :key='index' @change="onChange"  ></van-tab>
			</van-tabs>
			<!-- <view  v-for="(item,index) in topview" :key='index' class="a>
				<text class="t"></text>
			</view> -->
		</view>
		<view>
			<view class="centerview" v-for="(item,index) in datacenter" :key=index>
							<image :src="imageurl+item.photo"  class="leftimagurl" />
							<view class="rightview">
								<text class="righttextone">{{item.product_name}}</text>
								<text class="righttexttow">{{item.product_desc}}</text>
								<text class="pricetext">{{item.volume}}</text>
								<view class="rightbotview">
									<text class="moneytext">￥</text>
									<text class="textmontprice">{{item.price}}</text>
									<text class="quarry">明日达</text>
									<image src="http://192.168.0.107:8088/images/cart.png" class="iconadd" />
								</view>
							</view>
						</view>
		</view>
	</scroll-view>
</template>

<script>
	export default {
		data() {
			return {
				topview: '',
				datacenter:'',
				imageurl:'http://192.168.0.107:8088/',
				active:1
			}
		},
		methods: {
			prouctdata() {
				uni.request({
					url: 'http://192.168.0.107:8088/data/sub_category_list_0.json',
					success: (res) => {
						this.topview = res.data
						this.datacenter = res.data[0].productGroup
						console.log(this.topview ,66666)
					}
				});
			},
			onChange(){
				console.log(456456)
				 // wx.showToast({
				 //      title: `切换到标签 ${event.detail.name}`,
				 //    });
			}
		},
		created() {
			this.prouctdata()
		}
	}
</script>

<style scoped>
.centertxte{
	display: flex;
	flex-direction: row;
	overflow: hidden;
	white-space: nowrap;
	overflow-x: auto;
	height: 40px;
}
.allniu{
	width: 120px;
	text-align: center;
	background-color: #007AFF;
	margin-left: 10px;
}
.ttt{
	width: 120px;
	height: 30px;
	display: inline-block;
}
.centerview{
	display: flex;
	flex-direction: row;
	height: 130px;
	border-bottom: 1px solid #C0C0C0;
	padding-top: 15px;
}
.leftimagurl{
	width: 200upx;
	height: 200upx;
}
.rightview{
	display: flex;
	flex-direction: column;
	margin-left: 5px;
	width: 252px;
}
.righttextone{
	font-size: 14px;
	color: #555;
}
.righttexttow{
	color: #BBBABB;
	font-size: 11px;
	margin-top: 5px;
}
.pricetext{
	font-size: 11px;
	color: #C0C0C0;
	margin-top: 20px;
	}
.rightbotview{
	margin-top: 15px;
	display: flex;
	flex-direction: row;
}
.moneytext{
	font-size: 13px;
	color: #F0AD4E;
	margin-top: 3px;
}
.textmontprice{
	width: 40px;
	font-size: 16px;
	color:#F0AD4E ;
}
.quarry{
	font-size: 12px;
	width: 41px;
	height: 18px;
	background-color: #F0AD4E;
	color: #FFFFFF;
	margin-left: 15px;
	margin-top: 3px;
}
.iconadd{
	position: relative;
	width: 30px;
	height: 30px;
	left: 153px;
	top: -3px;
	}
</style>
