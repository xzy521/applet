<template>
	<scroll-view>
		<!-- 轮播 -->
		<swiper class="swip"  :indicator-dots="true" :autoplay="autoplay" :interval="interval" :duration="duration"
		 indicator-color="#cccc" indicator-active-color="red">
			<swiper-item v-for="(item,index) in bannurl" :key=index>
				<image :src="surl+item" class="imagesss" />
			</swiper-item>
		</swiper>
		<!-- 详情 -->
		<view class="delview">
			<text class="delvonetext">{{nametitel}}</text>
			<text class="delvtowtext">{{product_desc}}</text>
			<text class="pricead">{{price}}</text>
			<view class="allrow" >
				<!-- <view class="kgcd">{{item.volume}}</view> -->
				<view class="rightkgcdd" v-for="(item,index) in gkgsd" :key = 'index'>
					<view class="prkghk">{{item.volume}}</view>
					</view>
			</view> 
			<text class="botttext">{{sendTimeMsgs}}</text>
			<text class="zhottext">{{refundRule}}</text>
		</view>
		<!-- 表格数据 -->
		<view class="tabview"  >
			<view class="viewall">
				<text class="cz">{{prinfi.origin}}</text>
				<text class="cz">{{prinfi.originMsg}}</text>
			</view>
			<view class="viewall">
				<text class="czfx">{{prinfi.store}}</text>
				<text class="czfx">{{prinfi.storeMsg}}</text>
			</view>
			<view class="viewall">
				<text class="cz">{{prinfi.explain}}</text>
				<text class="cz">{{prinfi.explainMsg}}</text>
			</view>
		</view>
		<!-- 图片 -->
		<view class="viewallimg">
			<image :src='surl+item' v-for="(item,index) in imgs" mode="widthFix" class="scay" :key="index" />
		</view>
	</scroll-view>
</template>

<script>
	export default {
		data() {
			return {
				bannurl: '',
				autoplay: true,
				interval: 2000,
				duration: 500,
				surl: 'http://192.168.0.107:8088/',
				imgs:'',
				prinfi:'',
				refundRule:'',
				price:"",
				nametitel:'',
				prkgck:"",
				sendTimeMsgs:'',
				gkgsd:'',
			}
		},
		methods: {
			  onLoad: function(options) {    
			       console.log(options.prod)
				   this.nametitel = options.name
			      uni.request({
			      	url: 'http://192.168.0.107:8088/data/good_detail_'+options.prod+'.json',
			      	success: (res) => {
			      		this.bannurl = res.data.templatePhoto
						this.imgs = res.data.templateInfo.desc_imgs
						this.prinfi = res.data.templateInfo.pro_info
						this.refundRule = res.data.refundRule
						this.price = res.data.productInfo.price
						this.product_desc = res.data.productInfo.product_desc
						// this.prkgck = res.data.productItem[1].volume
						this.sendTimeMsgs = res.data.sendTimeMsg
						this.gkgsd = res.data.productItem
			      		console.log(res.data, 3333);
			      	}
			      });
			}
			  
		
		},
		mounted() {
			// this.onyy()
		}
	}
</script>

<style scoped>
	.swip{
		width: 100%;
		height: 355px;
		}
.imagesss {
		width: 752rpx;
		height: 355px;
		/* margin-left: 55px; */
	}
.delview{
	width: 365px;
	height: 250px;
	background-color: #FFFFFF;
	margin-left: 30px;
	/* margin-top: -20px; */
	position: relative;
	top: -50px;
	border-radius: 20px;
	display: flex;
	flex-direction: column;
	text-align: center;
}
.delvonetext{
	font-size: 18px;
	margin-top: 30px;
}
.delvtowtext{
	color: #C0C0C0;
	margin-top: 3px;
}
.pricead{
	margin-top: 10px;
	font-size: 24px;
	color: #FF8000;
}
.allrow{
	width: 100%;
	height: 51px;
	display: flex;
	flex-direction: row;
	/* margin-left: 60px; */
	justify-content: center;
	margin-top: 5px;
}
.kgcd{
	width: 60px;
	height: 34px;
	padding-top: 9px;
	text-align: center;
	background-color: #FFFFFF;
	font-weight: 700;
	color:#292927 ;
	border-radius: 8px;
	
}
.rightkgcdd{
	width: 135px;
	height: 34px;
	padding-top: 9px;
	text-align: center;
	background-color:#FFB200;
	color: #FFFFFF;
	font-size: 11px;
	display: flex;
	flex-direction: row;
	border-radius: 6px;
	margin-left: 20px;
}
.kggg{
	font-size: 16px;
}
.prkghk{
	margin-top: 5px;
	font-size: 14px;
	margin-left: 2px;
	width: 100%;
	text-align: 100%;
}
.botttext{
	font-size: 10px;
	color: #C0C0C0;
	margin-top: 10px;
}
.zhottext{
	margin-top: 20px;
	font-size: 16px;
}
.tabview{
	display: flex;
	flex-direction: column;
}
.viewall{
	width: 400px;
	height: 30px;
	margin-left: 7px;
	display: flex;
	flex-direction: row;
}
.cz{
	display: block;
	width: 50%;
	border: 1px solid #DCDCDC;
	padding-left: 30px;
	box-sizing: border-box;
	background-color: #F7F7F7; 
} 
.czfx{
	display: block;
	width: 50%;
	border: 1px solid #DCDCDC;
	padding-left: 30px;
	box-sizing: border-box;
}
.viewallimg{
	width: 400px;
	margin-left: 7px;
}
.scay{
	width: 100%;
	margin-bottom: -4px;
}
</style>
