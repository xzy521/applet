<template>
	<scroll-view>
		<view>
			<swiper class="swiper" :indicator-dots="true" :autoplay="autoplay" :interval="interval" :duration="duration"
			 indicator-color="#cccc" indicator-active-color="red">
				<swiper-item v-for="(item,index) in bannurl" :key=index>
					<image :src="surl+item" class="imagesss" mode="widthFix" />
				</swiper-item>
			</swiper>
		</view>
		<!-- 中间10个功能 -->
		<view>
			<!-- 上边 -->
			<view class="onecenter">
				<view class="centercenterone" v-for="(item,index) in centerten" :key=index>
					<image :src="surl+'/images/'+item.urlicon" class="centerurl" />
					<text class="centtext">{{item.title}}</text>
				</view>
			</view>
			<!-- 下边 -->
			<view class="onecenter">
				<view class="centercenterone" v-for="(item,index) in centertentow" :key=index>
					<image :src="surl+'/images/'+item.urlicon" class="centerurl" />
					<text class="centtext">{{item.title}}</text>
				</view>
			</view>
		</view>
		<!-- 热销榜 -->
		<view class="hot-set">
			<view class="hot-viewone">
				热销榜
			</view>
			<view class="fore-hot">
				受欢迎 好评高 有格调 还实惠
			</view>

			<view class="hot-setone">

				<view class="ytone" v-for="(item,index) in datahotset" :key='index'>
					<navigator open-type="redirect" :url="urlget(item.product_id,item.title)">
						<image :src='surl+item.image' class="imgyt" />
						<view class="sltext">
							{{item.subtitle}}
						</view>
						<view class="terts">
							{{item.title}}
						</view>
					</navigator>
					<view class="botvie">
						<view>{{item.price}}/{{item.volume}}
							<image src="http://192.168.0.107:8088/images/cart.png" class="icontt" @click="addshop(item.product_id,item.image,item.subtitle,item.title,item.price,item.volume,1,false)" />
						</view>
					</view>
				</view>

			</view>

		</view>
		<!-- 限时特惠 -->
		<view class="hot-set">
			<view class="hot-viewone">
				限时特惠
			</view>
			<view class="fore-hot">
				无需精打细算，怎么买都划算
			</view>
			<view class="hot-setone">
				<view class="ytone" v-for="(item,index) in datahotsetxsth" :key='index'>
					<navigator open-type="redirect" :url="urlget(item.product_id,item.title)">
					<image :src='surl+item.image' class="imgyt" />
					<view class="sltext">
						{{item.subtitle}}
					</view>
					<view class="terts">
						{{item.title}}
					</view>
					</navigator>
					<view class="botvie">
						<view>{{item.price}}/{{item.volume}}
							<image src="http://192.168.0.107:8088/images/cart.png" class="icontt" @click="addshop(item.product_id,item.image,item.subtitle,item.title,item.price,item.volume,1,false)"  />
						</view>
					</view>
				</view>
			</view>
		</view>
		<!-- 每周上新 -->
		<view class="hot-set">
			<view class="hot-viewone">
				每周上新
			</view>
			<view class="fore-hot">
				<text class="textleft">时令现货，精选优品</text>
				<navigator open-type="redirect" class="moretext" :url="pdurl+'?prod=480'">更多</navigator>
			</view>
			<view class="hot-setone">
				<view class="ytone" v-for="(item,index) in datahotnew" :key='index'>
					<navigator open-type="redirect" :url="urlget(item.product_id,item.title)">
					<image :src='surl+item.image' class="imgyt" />
					<view class="sltext">
						{{item.subtitle}}
					</view>
					<view class="terts">
						{{item.title}}
					</view>
					</navigator>
					<view class="botvie">
						<view>{{item.price}}/{{item.volume}}
							<image src="http://192.168.0.107:8088/images/cart.png" class="icontt" @click="addshop(item.product_id,item.image,item.subtitle,item.title,item.price,item.volume,1,false)"  />
						</view>
					</view>
				</view>
			</view>
		</view>
		<!-- 时令水果 -->
		<view class="hot-set">
			<view class="hot-viewone">
				时令水果
			</view>
			<view class="fore-hot">
				<text class="textleft">季节尝鲜，自然特色</text>
				<navigator open-type="redirect" class="moretext" :url="pdurl+'?prod=0'">更多</navigator>
			</view>
			<view class="hot-setone">
				<view class="ytone" v-for="(item,index) in datahotfruits" :key='index'>
					<navigator open-type="redirect" :url="urlget(item.product_id,item.title)">
					<image :src='surl+item.image' class="imgyt" />
					<view class="sltext">
						{{item.subtitle}}
					</view>
					<view class="terts">
						{{item.title}}
					</view>
					</navigator>
					<view class="botvie">
						<view>{{item.price}}/{{item.volume}}
							<image src="http://192.168.0.107:8088/images/cart.png" class="icontt" @click="addshop(item.product_id,item.image,item.subtitle,item.title,item.price,item.volume,1,false)"  />
						</view>
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
				background: ['color1', 'color2', 'color3'],
				autoplay: true,
				interval: 2000,
				duration: 500,
				surl: 'http://192.168.0.107:8088/',
				datahotset: '',
				bannurl: '',
				datahotsetxsth: '',
				datahotnew: '',
				datahotfruits: '',
				accarr: '',
				pdurl:'../../pages/index/morenew',
				sharr: [],
				centerten: [{
					"title": '每周上新',
					'urlicon': 'week.png'
				}, {
					"title": '新客专享',
					'urlicon': 'new.png'
				}, {
					"title": '天天直播',
					'urlicon': 'play.png'
				}, {
					"title": '摇一摇',
					'urlicon': 'shake.png'
				}, {
					"title": '限时特惠',
					'urlicon': 'limit.png'
				}, ],
				centertentow: [{
					"title": '低温素食',
					'urlicon': 'low.png'
				}, {
					"title": '品质肉禽',
					'urlicon': 'meat.png'
				}, {
					"title": '新鲜水果',
					'urlicon': 'fruit.png'
				}, {
					"title": '粮油干货',
					'urlicon': 'gh.png'
				}, {
					"title": '生活水饮',
					'urlicon': 'water.png'
				}, ],
			}
		},
		methods: {
			iamgurl() {
				uni.request({
					url: 'http://192.168.0.107:8088/data/fruits.json',
					success: (res) => {
						this.datahotset = res.data.bannerTags[0].content
						this.datahotsetxsth = res.data.bannerTags[1].content
						this.datahotnew = res.data.bannerTags[2].content
						this.datahotfruits = res.data.bannerTags[3].content
						this.bannurl = res.data.banners
						console.log(this.datahotset, 11111111111111); 
					}
				});
			},
			// 时令现货更多
			morenew() {
				console.log("时令现货")
			},
			urlget(id,name) {
				return ('../../pages/delies/cherry?prod=' + id +'&name='+name)

			},
			addshop(prod, imgurl, tile, bb, price, kg, numb,isf) {
				console.log(123,prod, imgurl, tile, bb, price, kg, numb,isf)
				let sum =''
				let accarr = ''
				uni.getStorage({
					key: 'shoparr',
					success: (res) => {
						accarr = res.data
						// console.log(accarr, 22222)
						if (accarr) {
							for (let i = 0; i < accarr.length; i++) {
								// console.log(i)
								if (accarr[i].prodd == prod) {
									accarr[i].num++
									sum++
									
								}
							}
							if(sum==0){
									// console.log("---+++++")
									accarr.push({"prodd":prod,"img": imgurl,"til": tile,"teb": bb,"kgdw": kg,"num":numb,"price":price,"istroe":isf})
									uni.setStorage({
										key: 'shoparr',
										data: accarr,
										success: (resp) => {
											// console.log(resp, 99999)
										}
										
									})
								
							}else{
								uni.setStorage({
									key: 'shoparr',
									data: accarr,
									success: (resp) => {
										// console.log(resp, 99999)
									}
								
								})
							}
						} else {
							// console.log("+++++")
							let asd = []
							asd.push({
								"prodd": prod,
								"img": imgurl,
								"til": tile,
								"teb": bb,
								"kgdw": kg,
								"num": numb,
								"price":price,
								"istroe":isf
							})
							uni.setStorage({
								key: 'shoparr',
								data: asd,
								success: (resp) => {
									// console.log(resp, 99999)
								}

							})
							console.log("222225555")
						}
					}

				})

				// 		uni.setStorage({
				// 			key: 'shoparr',
				// 			data: '',
				// 			success: (resp) => {
				// 				console.log(resp, 99999)
				// 			}

				// 		})


				// console.log(imgurl, tile, bb, price, kg, '888888')
			},





		},
		created() {
			this.iamgurl()
		}
	}
</script>

<style scoped>
	.imagesss {
		width: 750rpx;
		height: 450rpx;
	}
	/* .swiper{
		height: 450rpx;
	} */
	.hot-set {
		flex-direction: column;
		margin-top: 60px;
	}

	.hot-viewone {
		font-size: 22px;
		font-weight: 700;
		text-align: center;
	}



	.fore-hot {
		/* margin-left: 120px; */
		text-align: center;
		font-size: 14px;
	}

	.textleft {
		position: relative;
		left: 10px;
	}

	.ytone {
		display: flex;
		flex-direction: column;
		height: 200px;
		width: 140px;
		margin-right: 10px;
		padding-left: 5px;
	}

	.imgyt {
		width: 120px;
		height: 120px;
		margin-left: 5px;
	}

	.textsss {
		flex-direction: column;
	}

	.sltext {
		overflow: hidden;
		text-overflow: ellipsis;
		white-space: nowrap;
		font-weight: 600;
		font-size: 14px;
	}

	.terts {
		text-align: center;
		overflow: hidden;
		text-overflow: ellipsis;
		white-space: nowrap;
		font-size: 12px;
		color: #C0C0C0;
	}

	.botvie {
		text-align: center;
		color: #F0AD4E;
	}

	.icontt {
		width: 30px;
		height: 30px;
		position: relative;
		top: 10px;
	}

	.hot-setone {
		display: flex;
		flex-direction: row;
		overflow: hidden;
		white-space: nowrap;
		overflow-x: auto;
	}

	.moretext {
		width: 60px;
		position: relative;
		left: 360px;
		top: -20px;
	}

	.onecenter {
		display: flex;
		flex-direction: row;
		/* text-align: center; */
		margin-top: 35px;
	}

	.centercenterone {
		display: flex;
		flex-direction: column;
		margin-left: 15px;
		margin-right: 18px;
	}

	.centerurl {
		width: 50px;
		height: 50px;
	}

	.centtext {
		font-size: 12px;
	}
</style>
