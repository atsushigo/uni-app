<template>
	<view class="content">
		<view>
			<ynGallery 
			 :galleryheight="145" 
			  bkstart="#000000" 
			  bkend="#000000" 
			 :imgviewwidth="95" 
			 :imgviewheight="105" 
			 :showbadge="true"
			  badegtype="trian" 
			  badegwidth="25" 
			  badegheight="25" 
			 :showdec="true" 
			 :images="testimgs" 
			 @clickimg="onclickimg">
			</ynGallery>
			<text style="font-size: 15px;">
				您在 {{Msg}} 頁面
			</text>
		</view>
		<!-- ----------------- -->
		<view class="" style="background-color:white">
			<!-- <image class="logo" src="/static/logo.png"></image> -->
			<!-- 白色區域文字 -->
			<view >
				<text class="title">{{title}}</text>
				<view v-for="(item,index) in items" style="">
					<li>{{item.name}}  {{item.mail}}</li>
				</view>
			</view>
			<text class="cuIcon-hotfill lg"></text>
		</view>
		<!-- ------- -->
		
        <!-- ----------------- -->
		<!-- 表格1 -->
		<view class="warp" >
				<view class="box">
					<view class="title">Json接口 Get測試</view>
					<view><a href="https://jsonplaceholder.typicode.com/posts">https://jsonplaceholder.typicode.com/posts</a></view>
					<t-table @change="change">
						<t-tr>
							<t-th>ID</t-th>
							<t-th>主題</t-th>
						</t-tr>   
					<!-- 用slice去取幾到幾個數 -->
						<t-tr v-for="item in tableList.slice(0,20)" :key="item.id">
							<t-td>{{ item.id }}</t-td>
							<t-td>{{ item.title }}</t-td>
						</t-tr>
					</t-table>
				</view>
				<!-- --------------- -->
				<data1></data1>
				<!-- ----------------------- -->
				<!-- 表格2 -->
				<view class="box">
					<view class="title">測試接口2</view>
					<view>	<a href="https://data.taipei/opendata/datalist/apiAccess?scope=resourceAquire&rid=549b3a9b-eb6c-4cb1-848b-8c238735e2db">https://data.taipei/opendata/datalist/apiAccess?scope=resourceAquire&rid=549b3a9b-eb6c-4cb1-848b-8c238735e2db</a></view>
					<t-table border="2" border-color="#95b99e" :is-check="true" @change="change">
						<t-tr font-size="20" color="#95b99e" align="center">
							<t-th align="center">姓名</t-th>
							<t-th align="center">經度</t-th>
							<t-th align="center">緯度</t-th>
							<t-th align="center">   </t-th>
						</t-tr>
						<t-tr font-size="12" color="#5d6f61" align="right" v-for="item in tableList1.slice(0,10)" :key="item.id">
							<t-td align="left">{{ item.NAME }}</t-td>
							<t-td align="left">{{ item.LATITUDE }}</t-td>
							<t-td align="left">{{ item.LONGITUDE }}</t-td>
							<t-td align="left"><button @click="edit(item)">编辑</button></t-td>
						</t-tr>
					</t-table>
				</view>
			</view>
		
		
		<view><br><br><br><br></view>
	</view>
</template>


<script>
	import ynGallery from 'components/YnComponents/ynGallery/ynGallery.vue'
	// -------------------
    import tTable from '@/components/t-table/t-table.vue';
    	import tTh from '@/components/t-table/t-th.vue';
    	import tTr from '@/components/t-table/t-tr.vue';
    	import tTd from '@/components/t-table/t-td.vue';
		// --------------------//
		// import {uniBadge} from '@dcloudio/uni-ui'
	export default {
		components: {
			ynGallery,
			tTable,tTh,tTr,tTd,
			// uniBadge
		},
		onLoad() {
			uni.request({
				url:'https://jsonplaceholder.typicode.com/posts',
				method:"GET",
				success: (res) => {
					this.tableList = res.data
				}
			});
			uni.request({
				url:'https://data.taipei/opendata/datalist/apiAccess?scope=resourceAquire&rid=549b3a9b-eb6c-4cb1-848b-8c238735e2db',
				method:"GET",
				success: (res) => {
					this.tableList1 = res.data.result.results
				}
			})
		},
		
		data() {
			return {
				sh: 0,
				Msg: "0",
				title: 'Hello',
				change:[],
				items:[
					{name:'Sam',mail:'123@gamil.com'},{name:'Yaris',mail:'1234@gamil.com'},{name:'Tim',mail:'12345@gamil.com'}
				],
				tableList:[],
				tableList1:[],
				
				// 画廊示例数据
				testimgs: [{
						url: "https://i2.wp.com/michaelbakerhomeloans.com/wp-content/uploads/2017/01/Waiting.jpg?fit=2000%2C1333&ssl=1"
					},
					{
						url: "data:image/jpeg;base64,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"
					},
					{
						url: "data:image/png;base64,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"
					},
					{
						url: "https://leggerhythms.org/wp-content/uploads/2019/04/callforpaper.jpg"
					},
					
				],
			}
		},
		methods: {
			
			
			
			
			onclickimg(imgviewobj) {
				if (imgviewobj.index != undefined)
					this.Msg = `${imgviewobj.index}`;
			},
			setimgs() {
				var imgs=[];
				for (let i in this.testimgs) {									
					 let imgobj={
						  dec:'',                   //图像描述信息
						  badeg:'',                 //角标文字
						  badegcolor:'#000000',     //角标颜色
						  url:'',                   //图源  
						  dominant:''               //主色  
					};
					imgobj.url=this.testimgs[i].url;
					imgobj.dominant = this.retcolor(); //随机主色
					imgobj.dec = i; //描述  
					imgobj.badeg = i; //角标文字
					imgobj.badegcolor = (i % 2) == 0 ? 'red' : 'LimeGreen'; //角标颜色
					
					imgs.push(imgobj)
				}
				this.testimgs=imgs;
			},
			retcolor() {
				let color = '#' + ('00000' + (Math.random() * 0x1000000 << 0).toString(16)).substr(-6);
				return color;
			}
		}
	}
</script>

<style>
	.content {
		text-align: center;
		height: 400upx;
	}

	.logo {
		height: 100upx;
		width: 100upx;
		margin-top: 350upx;
		margin-bottom: 10upx;
		border-radius: 50upx;
	}

	.title {
		font-size: 36upx;
		color: #8f8f94;
	}
</style>