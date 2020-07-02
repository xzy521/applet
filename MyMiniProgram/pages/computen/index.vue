<template>
	<view class="bigvie">
		<!-- 左边 -->
		<view class="leftview">
			<view :class="antive===index? 'leftt' :'lefttext' "  v-for="(item,index) in leftdataone" :key="index" @click="clickleft(item.id,index)">{{item.name}}</view>
		</view>
		<!-- 右边 -->
		<view class="rightview">
			<view class="rightbott" v-for="(item,index) in dataright" :key='index'>
				<view class="tilite">{{item.className.name}}</view>
				<view class="bigcenter">
				<view class="ss" v-for="(items,indexs) in item.classGroup" :key="indexs" >
					<image :src="imagurl+items.class_photo" class="imagesc" />
					<text class="textaaa">{{items.name}}</text>
				</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				leftdataone:'',
				antive:0,
				dataright:'',
				imagurl:'http://192.168.0.107:8088/'
			}
		},
		methods: {
			leftdata(){
				uni.request({
					url:"http://192.168.0.107:8088/data/category_list.json",
					success: (res) =>{
						this.leftdataone = res.data
					}
				})
			},
			clickleft(prod,index){
				this.antive = index
				uni.request({
					url:'http://192.168.0.107:8088/data/category_list_'+prod+'.json',
					success:(resp)=>{
						this.dataright = resp.data
					}
				})
			}
		},
		mounted() {
			this.leftdata()
			this.clickleft(478,0)
		}
	}
</script>

<style scoped>
	.bigvie{
		display: flex;
		flex-direction: row;
	}
	.leftview{
		width: 24%;
		/* background-color: red; */
	}
	.lefttext{
		height: 40px;
		background-color:#F7F8FA ;
		text-align: center;
		padding-top: 20px;
	}
	.leftt{
		height: 40px;
		background-color:#FFFFFF ;
		text-align: center;
		padding-top: 20px;
		color: black;
		border-left: 2px solid red;
		}
	.rightview{
		width: 75%;
		/* background-color: #4CD964; */
	}
	.rightbott{
		display: flex;
		flex-direction: column;
	}
	.imagesc{
		width: 80px;
		height: 80px;
	}
	.textaaa{
		width: 80px;
		text-align: center;
		}
	.bigcenter{
		display: grid;
		grid-template-columns: repeat(3,1fr);
		grid-template-rows: repeat(1,100px);
	}
	.tilite{
		width: 100%;
		text-align: center;
		font-weight: 700;
		margin-top: 10px;
	}
	.ss{
		display: flex;
		flex-direction: column;
	}
</style>
