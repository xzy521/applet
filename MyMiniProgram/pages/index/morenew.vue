<template>
	<scroll-view>
		<view class="heanderxinx">
			新鲜尝鲜
		</view>
		<view>
			<van-tabs :active="active " color="red" animated>
				<van-tab :title='item.name' v-for="(item,index) in topview" :key='index' @change="onChange">
					<view class="centtree">
						<text class="tet">综合</text>
						<text class="tet">销量</text>
						<text class="tet">价格</text>
					</view>
					<view>
						<view class="centerview" v-for="(items,indexs) in item.productGroup" :key='indexs'>
							<image :src="imageurl+items.photo" class="leftimagurl" />
							<view class="rightview">
								<text class="righttextone">{{items.product_name}}</text>
								<text class="righttexttow">{{items.product_desc}}</text>
								<text class="pricetext">{{items.volume}}</text>
								<view class="rightbotview">
									<text class="moneytext">￥</text>
									<text class="textmontprice">{{items.price}}</text>
									<text class="quarry">明日达</text>
									<image src="http://192.168.0.107:8088/images/cart.png" class="iconadd" @click="addshop(items.id,items.photo,items.product_desc,items.product_name,items.price,items.unit,1,false)" />
								</view>
							</view>
						</view>
					</view>
				</van-tab>
			</van-tabs>
		</view>
		
	</scroll-view>
</template>

<script>
	export default {
		data() {
			return {
				datacenter: '',
				imageurl: 'http://192.168.0.107:8088/',
				active: 0,
				topview: ''
			}
		},
		methods: {
			onLoad: function(options) {  
				options.prod
				uni.request({
					url: 'http://192.168.0.107:8088/data/sub_category_list_'+options.prod+'.json',
					success: (res) => {
						// this.datacenter = res.data[0].productGroup
						this.topview = res.data
						// console.log(this.datacenter, 2222222)
					}
				});
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
		mounted() {
			
		}
	}
</script>

<style scoped>
	.centerview {
		display: flex;
		flex-direction: row;
		height: 130px;
		border-bottom: 1px solid #C0C0C0;
		padding-top: 15px;
	}

	.leftimagurl {
		width: 200upx;
		height: 200upx;
	}

	.rightview {
		display: flex;
		flex-direction: column;
		margin-left: 5px;
		width: 252px;
	}

	.righttextone {
		font-size: 14px;
		color: #555;
	}

	.righttexttow {
		color: #BBBABB;
		font-size: 11px;
		margin-top: 5px;
	}

	.pricetext {
		font-size: 11px;
		color: #C0C0C0;
		margin-top: 20px;
	}

	.rightbotview {
		margin-top: 15px;
		display: flex;
		flex-direction: row;
	}

	.moneytext {
		font-size: 13px;
		color: #F0AD4E;
		margin-top: 3px;
	}

	.textmontprice {
		width: 40px;
		font-size: 16px;
		color: #F0AD4E;
	}

	.quarry {
		font-size: 12px;
		width: 41px;
		height: 18px;
		background-color: #F0AD4E;
		color: #FFFFFF;
		margin-left: 15px;
		margin-top: 3px;
	}

	.iconadd {
		position: relative;
		width: 30px;
		height: 30px;
		left: 153px;
		top: -3px;
	}

	.heanderxinx {
		width: 100%;
		height: 30px;
		background-color: #F8F8F8;
		color: #747474;
		text-align: center;
		padding-top: 3px;
	}
	.centtree{
		width: 100%;
		height: 28px;
		background-color: #F5F5F5;
		display: flex;
		flex-direction: row;
		justify-content: space-around;
	}
	.tet{
		display: block;
		font-size: 12px;
		padding-top: 5px;
	}
</style>
