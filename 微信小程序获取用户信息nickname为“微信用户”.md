**学习小程序的时候发现获取用户信息失败，最后发现是一下原因，个人感觉微信的错误提示不够清楚明了，简直是浪费开发者的时间。**
---

最近两天小程序用户登录获取到的用户微信名称都变成了"微信用户"，在网上找到的问题原因是getUserProfile API被收回微信社区

头像昵称填写能力可以获取用户头像和昵称直接上代码，如果有更好的方案请留言！！！！！！！！

![](https://raw.githubusercontent.com/janrone/bmages/main/wimg/d9f1932ceaa043878e8a189e2584c15d.png)

```
<template>
	<view>
		<button class="avatar-wrapper" open-type="chooseAvatar" @chooseavatar="onChooseAvatar">
			<image class="avatar" :src="avatarUrl"></image>
		</button>
		<view class="petName">
			<view class="petName_name">昵称</view>
			<input type="nickname" v-model="nickname" class="weui-input" placeholder="请输入昵称" />
		</view>
		<view class="ensure" @click="ascertain">确定</view>
	</view>
</template>

<script>
	const defaultAvatarUrl =
		'https://mmbiz.qpic.cn/mmbiz/icTdbqWNOwNRna42FI242Lcia07jQodd2FJGIYQfG0LAJGFxM4FbnQP6yfMxBgJ0F3YRqJCJ1aPAK2dQagdusBZg/0'
	export default {
		data() {
			return {
				avatarUrl: defaultAvatarUrl,
				nickname:''
			}
		},
		methods: {
			onChooseAvatar(e) {
				console.log(e);
				const {
					avatarUrl
				} = e.detail
				this.avatarUrl=avatarUrl
			},
			ascertain(){
				uni.navigateBack({
					delta:1
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.avatar-wrapper{
		height: 300rpx;
		text-align: center;
		display: flex;
		align-items: center;
		justify-content: center;
	}
	.avatar{
		width: 100rpx;
		height: 100rpx;
	}
	.petName{
		padding: 0 20rpx;
		height: 100rpx;
		display: flex;
		align-items: center;
		.petName_name{
			width: 150rpx;
		}
	}
	.ensure{
		position: fixed;
		bottom: 0;
		width: 100%;
		height: 80rpx;
		background: #07C160;
		color: #FFFFFF;
		display: flex;
		align-items: center;
		justify-content: center;
	}
</style>
```

版权声明：本文为CSDN博主「郭辰羽」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_49552046/article/details/127808212
