<template>
	<scroll-view>
		<view class="henader">
			<text>商品清单</text>
			<text>总重约20.25kg</text>
		</view>
		<!-- 下面主题内容 -->
		<view>
			<view class="onecenter" v-for="(item,index) in prouct" :key='index'>
				<van-checkbox :value='item.istroe' class="chckas" checked-color=" #F47E1F" icon-size="16px" @change="odd(index)" />
				<image :src="urlimg +item.img" class="imgss" />
				<view>
					<view class="rightile">
						<view class="righttileleft">{{item.teb}}</view>
						<view class="righttextkg">{{item.kgdw}}</view>
					</view>
					<view class="kgnum">{{item.kgdw}}</view>
					<view class="rightcentbot">
						<view class="price">￥{{item.price}}</view>
						<view class="rightrightadd">
							<view class="add" @click="lose(index)">-</view>
							<input type="text" class="centervie" disabled="true" v-model='item.num' />
							<!-- <view >{{item.num}}</view> -->
							<view class="add" @click="addone(index)">+</view>
						</view>
					</view>
				</view>
			</view>
		</view>
		<!-- 底部内容 -->
		<view class="footerview">
			<van-checkbox :value=isteur checked-color=" #F47E1F" icon-size="16px" @change="onchange" class="inpcall">全选</van-checkbox>
			<view class="allprice">￥{{allprice}}</view>
			<view class="payprie" @click="endpay">结算({{nnnu}})</view>
		</view>
	</scroll-view>
</template>

<script>
	export default {
		data() {
			return {
				prouct: '',
				urlimg: 'http://192.168.0.107:8088/',
				snum: '',
				isteur: false,
				allprice: 0,
				nnnu:0
			}
		},
		methods: {
			onShow: function(datalost) {
				uni.getStorage({
					key: 'shoparr',
					success: (res) => {
						this.prouct = res.data
					}
				})
			},
			addone(i) {
				this.prouct[i].num++
				uni.setStorage({
					key: 'shoparr',
					data: this.prouct,
					success: (resp) => {
						// console.log(resp, 99999)
					}

				})
			},
			lose(i) {
				this.prouct[i].num--
				uni.setStorage({
					key: 'shoparr',
					data: this.prouct,
					success: (resp) => {
						// console.log(resp, 99999)
					}

				})
				
			},
			onchange(event) {
				this.isteur = event.detail
				this.prouct.map(item => {
					if (this.isteur == true) {
						item.istroe = true
					} else {
						item.istroe = false
					}
				})

			},
			odd(i) {
				this.prouct[i].istroe = !this.prouct[i].istroe
				if (this.prouct[i].istroe == false) {
					this.isteur = false
				}
				uni.setStorage({
					key: 'shoparr',
					data: this.prouct,
					success: (resp) => {
						// console.log(resp, 99999)
					}
				})
				let s = 0
				let alls = 0
				let sc = 0
				for (let c = 0; c < this.prouct.length; c++) {
					if (this.prouct[c].istroe == false) {
						s++
					} else {
						sc++
						alls += parseFloat(this.prouct[c].price) * parseFloat(this.prouct[c].num)
					}

				}
				// console.log(sc,"sc")
				this.nnnu = sc
				if (s === 0) {
					this.isteur = true
				}
				// console.log(alls, "总价格")
				this.allprice = parseFloat(alls)
			},
			computers() {
				let s = 0
				let alls = 0
				let sc = 0
				for (let c = 0; c < this.prouct.length; c++) {
					if (this.prouct[c].istroe == false) {
						s++
					} else {
						sc++
						alls += parseFloat(this.prouct[c].price) * parseFloat(this.prouct[c].num)
					}

				}
				// console.log(sc,"sc++")
				this.nnnu = sc
				if (s === 0) {
					this.isteur = true
				}else{
					this.isteur = false
				}
				// console.log(alls, "总价格")
				this.allprice = parseFloat(alls)
			},
			// 结算
			endpay(){
				let arrt = ''
				for(let i=this.prouct.length-1;i>=0;i--){
					if(this.prouct[i].istroe == true){
						console.log(this.prouct[i].prodd)
						this.prouct.splice(i,1)
					}
					
				}
				console.log(this.prouct,9696969)
				uni.setStorage({
					key: 'shoparr',
					data: this.prouct,
					success: (resp) => {
						// console.log(resp, 99999)
					}
				})
			}

		},
		mounted() {
			this.computers()
		},
		updated() {
			this.computers()
		}
	}
</script>

<style scoped>
	.henader {
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		height: 35px;
		background-color: #EEEEEE;
		padding-top: 8px;
	}

	.chckas {
		margin-top: 43px;
		margin-left: 5px;
	}

	.onecenter {
		height: 110px;
		display: flex;
		flex-direction: row;
		padding-top: 10px;
		border-bottom: 1px solid #C0C0C0;
	}

	.imgss {
		width: 100px;
		height: 100px;
	}

	.rightile {
		display: flex;
		flex-direction: row;
		margin-top: 5px;
	}

	.righttileleft {
		font-size: 12px;
		font-weight: 600;
		width: 182px;
	}

	.righttextkg {
		margin-left: 62px;
		width: 40px;
		text-align: center;
		color: #646566;
	}

	.kgnum {
		color: #646566;
		font-size: 14px;
		margin-top: 5px;
	}

	.rightcentbot {
		display: flex;
		flex-direction: row;
		margin-top: 20px;
	}

	.rightrightadd {
		margin-left: 185px;
		display: flex;
	}

	.add {
		width: 20px;
		height: 20px;
		border: 1px solid #ccc;
		border-radius: 10px;
		text-align: center;
		color: #F47E1F;
		padding-top: -5px;
	}

	.centervie {
		width: 20px;
		text-align: center;
		color: #646566;
	}

	.price {
		color: #F47E1F;
	}

	.footerview {
		display: flex;
		flex-direction: row;
		height: 40px;
		padding-top: 14px;
		position: fixed;
		bottom:0;
		background-color: #F4F3F3;
		border-top: 2px solid #C0C0C0;
	}

	.inpcall {
		font-size: 14px;
		margin-left: 5px;
	}

	.allprice {
		width: 80px;
		text-align: center;
		margin-left: 180px;
		color: #F47E1F;
	}

	.payprie {
		width: 95px;
		height: 41px;
		background-color: #F47E1F;
		text-align: center;
		padding-top: 14px;
		margin-top: -16px;
		color: #FFFFFF;

	}
</style>
