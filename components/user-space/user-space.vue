<template>
	<view class="user-space-head u-f-ajc">
		<image :src="bgimagurl" mode="widthFix" lazy-load @tap.stop="changBgImg"></image>
		<view class="user-space-head-info u-f-ajc u-f-column">
			<image :src="userinfo.userpic" mode="widthFix" lazy-load></image>
			<view class="user-space-margin u-f-ac">
				{{userinfo.username}}
				<user-sex-age :sex="userinfo.sex" :age="userinfo.age"></user-sex-age>
			</view>
			<view class="icon iconfont user-space-head-btn user-space-margin" :class="[isguanzhu?'active':'icon-zengjia']" @tap.stop="guanzhu">
				{{isguanzhu?'已关注':'关注'}}
			</view>
		</view>
	</view>
</template>

<script>
	import userSexAge from '../../components/common/user-sex-age.vue';
	export default {
		components:{
			userSexAge
		},
		props:{
			userinfo:Object
		},
		data() {
			return {
				isguanzhu:this.userinfo.isguanzhu,
				bgimagurl:"../../static/bgimg/"+this.userinfo.bgimg+".jpg"
			}
		},
		computed:{
			// 未生效
			getBgImg(){
				return "../../static/bgimg/"+this.userinfo.bgimg+".jpg";
			}
		},
		methods:{
			//切换背景
			changBgImg(){
				console.log('changBgImg')
				let no = parseInt(this.userinfo.bgimg);
				this.userinfo.bgimg = no<4 ? ++no : 1;
				this.bgimagurl="../../static/bgimg/"+this.userinfo.bgimg+".jpg";
			},
			// 关注
			guanzhu(){
				this.isguanzhu=!this.isguanzhu;
			}
		}
	}
</script>

<style scoped>
.user-space-head{
	position:relative;
	height: 500upx;
	overflow: hidden;
}
.user-space-head>image{
	width: 100%;
}
.user-space-head-info{
	position: absolute;
	top:150upx;
}
.user-space-head-info>image{
	width:150upx;
	border-radius: 100%;
}
.user-space-head-info>view:first-of-type{
	color: #FFFFFF;
	font-size: 35upx;
	font-weight: bold;
	text-shadow: 2upx 2upx 10upx #333333;
}
.user-space-head-btn{
	background: #FFE933;
	color:#333333;
	border: 1upx solid #FFE933;
	padding: 0 15upx;
	border-radius: 10upx;
	font-size: 28upx;
}
.active{
	background: none;
	color: #FFFFFF;
	border: 1upx solid #FFFFFF;
}	
</style>
