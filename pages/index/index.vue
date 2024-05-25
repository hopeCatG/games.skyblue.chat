<template>
	<div class="games" ref="gamesRef">
		<view class="img_bg" :style="`background: linear-gradient(rgb(175 162 162 / 50%), rgb(0 0 0)),
				url('${gamesImg[id]}') no-repeat center center/cover;`"></view>
			<!-- nav -->
			<view class="flex justify-between padding-tb-sm justify-between nav padding-sm">
				<image @click="showToastF('返回！')" style="width: 24rpx;height: 32rpx;" class="flipped-image"
					src="../../static/right.png" mode="">
				</image>
				<view class="flex">
					<image @click="showToastF('分享！')" style="width: 68rpx;height: 56rpx;" src="../../static/share.png"
						mode=""></image>
					<image @click="showToastF('收藏！')" class="margin-left-sm" style="width: 68rpx;height: 56rpx;"
						src="../../static/collect.png" mode=""></image>
				</view>
			</view>
			<view style="height: 80rpx;"></view>
			<view class="content padding-sm flex flex-direction">
				<!-- 介绍 -->
				<view class="margin-top-xs flex justify-between flex-sub">
					<view class="flex">
						<image class="radius-8" style="width: 208rpx;height: 290rpx;" :src="gamesImg[id]"></image>
						<view class="padding-left-sm flex flex-direction justify-between">
							<view>
								<view style="width: 300rpx;" class="text-white text-xl text-bold text-cut"
									@click="showModal = true">
									{{gamesName[id]}}
								</view>
								<view class="flex margin-top-xs" @click="showModal = true">
									<image class="margin-top-xs" style="width: 12rpx;height: 12rpx;"
										src="../../static/round_ball.png" mode=""></image>
									<text style="width: 300rpx;"
										class="text-gray text-sm margin-left-xs text-cut2">{{gamesContent[id]}}</text>
								</view>
								<view class="flex margin-top-xs text-white text-sm modal-box">
									<text class="text-gray text-sm margin-left-xs" @click="showModal = true">游戏介绍</text>
									<image class="margin-top-xs" style="width: 18rpx;height: 16rpx;"
										src="../../static/right.png" mode=""></image>
									<!-- 模特框 -->
									<view v-if="showModal" :class="['modal','padding-smx',showModal ? 'show' : 'hide']"
										@click="showModal = false">
										<view class="flex justify-between  text-white">
											<text class="text-xl text-bold">{{gamesName[id]}}</text>
											<image src='../../static/closure.png' style="width: 26rpx;height: 26rpx;"
												mode=""></image>
										</view>
										<view class="text-white indent">
											新的生命之地。狩猎, 就是本能! 在人气作品「Monster Hunter: World」里, 地形和环境生物, 甚至魔物的生态系统都能被利用,
											用一切手段挑战巨大的魔物。在新建构的「Monster Hunter: World」中, 可以体验到你一直期盼的极致猎人生活。
											在壮丽的大自然中与魔物进行一场史诗式的决斗。

											玩家化身成猎人, 接受任务狩猎生活栖息在各种环境中的魔物。利用狩猎魔物取得的材料, 制作更强的武器和防具, 挑战更强大的魔物。

											在游戏「Monster Hunter: World」中,玩家可以体验终极的狩猎生活,活用新建构的世界中各种各样的地形与生态环境享受狩猎的惊喜与兴奋。
									</view>
										</view>
								</view>
							</view>


							<image style="width: 180rpx;height: 50rpx;" src="../../static/handle.png" mode=""></image>
						</view>
					</view>

					<view class="flex flex-direction justify-between text-sm">
						<view class="score-box flex flex-direction justify-center text-center">
							<text class="text-green text-20 text-bold">9.4</text>
							<text class="text-green text-sm text-bold">评分</text>
						</view>
						<view class="flex text-gray justify-center ">
							<text class="align-self-center">由</text>
							<view class="cu-avatar sm round margin-lr-xs "
								style="background-image:url(../../static/user.png)">
							</view>
							<text class="align-self-center">分享</text>
						</view>
					</view>
				</view>
				<!-- 介绍 end -->

				<!-- tabs -->
				<view class="tabs">
					<view class="tab flex flex-direction radius-8 justify-center text-center" v-for="(i,index) in tabs"
						:key="index">
						<text class="text-green text-sm text-bold">{{i}}</text>
					</view>
				</view>

				<!-- 轮播图 -->
				<view class="margin-top-sm swiper-box">
					<!-- 正在玩 -->
					<view :class="['swiper-bg','text-black',show ? 'show' : 'hide']">
						<image class="wh100" src="../../static/swiper-bg.png" mode=""></image>
						<view class="text-box">
							<text class="text-green text-bold text-lg">94</text>
							<text class="text-df margin-left-xs">人正在玩</text>
						</view>
					</view>

					<!-- 轮播图 -->
					<swiper class="banner-container" :autoplay="false" :indicator-dots="false" :circular="true"
						:interval="3000" :duration="500" @change='show = false' @animationfinish='show = true'
						previous-margin="25rpx" next-margin="25rpx">
						<block v-for="(item,index) in imgUrls[id]" :key="index">
							<swiper-item class="banner-item">
								<view class="banner-box">
									<image class="banner-img " :src="item"></image>
								</view>
							</swiper-item>
						</block>
					</swiper>


				</view>
				<!-- 开始游戏 -->
				<view v-if="type == 0" class="button-game radius-8 ov-hidden margin-top-sm flex justify-center "
					@click="showToastF('开始游戏！')">
					<image class="align-self-center margin-right-xs" style="width: 48rpx;height: 48rpx;"
						src="../../static/game_icon.png" mode=""></image>
					<text class="align-self-center text-black text-bold text-lg">开始游戏</text>
				</view>
				<view class="flex  text-center padding-tb-sm" v-else>
					<view class="basis-sm download flex flex-direction justify-center" @click="showToastF('下载游戏！')">
						<view class="text-black text-lg">下载游戏</view>
						<view class="text-gray">游戏图标安装在桌面上</view>
					</view>
					<view class=" button2 flex flex-sub justify-center " @click="showToastF('开始游戏！')">
						<image class="align-self-center margin-right-xs" style="width: 48rpx;height: 48rpx;"
							src="../../static/game_icon.png" mode=""></image>
						<text class="align-self-center text-black text-bold text-lg">开始游戏</text>
					</view>
				</view>
				<!-- 版本 -->
				<view v-if="type == 0" class="Version padding-sm margin-tb-sm flex justify-between"
					@click="showToastF('其它版本！')">
					<view class="flex">
						<image style="width: 48rpx;height: 48rpx;" src="../../static/Version.png" mode=""></image>
						<text style="margin-top: -5rpx;" class="text-gray text-df align-self-center ">其它版本</text>
					</view>
					<image class="align-self-center " style="width: 24rpx;height: 32rpx;" src="../../static/right.png"
						mode="" />
				</view>
				<view v-else class="Version Version-else padding-sm margin-tb-sm flex justify-between">
					<view class="flex flex-sub justify-center" @click="showToastF('其它版本！')">
						<view class="flex margin-right-sm">
							<text style="margin-top: -5rpx;" class="text-gray text-df align-self-center ">其它版本</text>
						</view>
						<image class="align-self-center " style="width: 24rpx;height: 32rpx;"
							src="../../static/right.png" mode="" />
					</view>
					<view class="flex flex-sub justify-center " @click="showToastF('游戏攻略！')">
						<view class="flex margin-right-sm">
							<text style="margin-top: -5rpx;" class="text-gray text-df align-self-center ">游戏攻略</text>
						</view>
						<image class="align-self-center " style="width: 24rpx;height: 32rpx;"
							src="../../static/right.png" mode="" />
					</view>
				</view>
				<!-- 评价 -->
				<image class="margin-tb-sm" style="width: 88rpx;height: 44rpx;" src="../../static/evaluate.png" mode="">
				</image>
				<view class="Version padding-sm margin-bottom-sm" v-for="(eve,eveIndex) in evaluateArr" :key="eveIndex">
					<!-- 用户info -->
					<view class="flex justify-between">
						<view class="flex flex-sub ">
							<view class="cu-avatar sm round margin-right-xs "
								:style="`background-image:url(${eve.user_info.active});width:64rpx;height:64rpx;`">
							</view>
							<view class="flex flex-direction margin-left-xs">
								<view class="flex">
									<text class="text-white text-df text-8">{{eve.user_info.name}}</text>
									<image v-if="eve.user_info.is_vip" class="margin-left-xs"
										style="width: 104rpx;height: 40rpx;" src="../../static/SVIP.png" mode="">
									</image>
								</view>
								<text class="date margin-top-xs">{{eve.date}}</text>
							</view>
						</view>
						<image style="width: 40rpx;height: 40rpx;" src="../../static/more.png" mode=""></image>
					</view>
					<!-- 评论内容 -->
					<view class="text-cut2 margin-tb-sm ">
						{{eve.content}}
					</view>
					<view class="grid-3 gap-10">
						<view class="radius-8 ov-hidden " v-for="(img,img_index) in eve.images" :key="img_index">
							<image class="content-img wh100" @click="click_img(img_index,eve.images)"  :src="img" mode="">
							</image>
						</view>
					</view>
					<!-- 评分 留言 -->
					<view class="flex justify-between score_box padding-xs">
						<view class="flex">
							<image v-for="(score,score_index) in 5" :key="score_index"
								:src="`../../static/${eve.score >= score ?'yes' : 'no'}.png`" mode=""></image>
						</view>
						<view class="flex">
							<view class="flex">
								<image src="../../static/comment.png" mode=""></image>
								<text class="margin-left-xss text-8">{{eve.comment}}</text>
							</view>
							<view class="flex margin-left-sm" @click="like_click(eve)">
								<image :class="[eve.click ? 'rotateScale_init' : '']"
									:src="`../../static/${eve.click ? 'like-active' : 'like'}.png`" mode=""></image>
								<text class="margin-left-xss text-8">{{eve.like}}</text>
							</view>
						</view>
					</view>
				</view>
			</view>
	</div>

	<!-- 返回顶部 -->
	<view :class="['back_to_top' , showTOP ? 'show' : 'hide']">
		<view class="margin-bottom-sm" @tap="scrollToTop">
			<image class="wh100" src="../../static/back_to_top.png" mode=""></image>
		</view>
		<image style="width: 72rpx;height: 72rpx;" src="../../static/publish.png" mode=""></image>
	</view>


</template>

<script lang="ts">
	import {
		reactive,
		ref,
		toRefs,
		onMounted,
		onBeforeUnmount
	} from 'vue'
	const type = 0;
	export default {
		name: 'index',
		data() {
			return {
				type: 0,
				id: 0
			}
		},
		setup() {
			const TOP = 250; // 滚动条监听值
			let debounceTimer = null; //滚动条节流
			const showTOP = ref(false);
			const showModal = ref(false);
			const gamesRef = ref(null);
			const state = reactive({
				gamesName: [
					'怪物猎人世界怪物猎人世界怪物猎人世界怪物猎人世界',
					'侠盗猎车手5（GTA 5）豪华版'
				],
				gamesContent: [
					'怪物猎人世界怪物猎人世界怪物猎人世界怪物猎人世界',
					'欢迎来到洛圣都!'
				],
				gamesImg: [
					'../../static/game.webp',
					'https://static.88gog.com/res/4854363a-cf35-40e6-af23-58f0e206ff34.png',
				],
				tabs: ['动作', '合作', '多人', '开放世界', '角色扮演', '第三人称'],
				imgUrls: [
					[
						'../../static/swiper1.jpg',
						'../../static/swiper2.jpg',
						'../../static/swiper3.jpg',
						'../../static/swiper4.jpg',
					],
					[
						'https://static.88gog.com/res/6ea65967-e6f5-46b6-b680-ddc4e3e29608.jpg',
						'https://static.88gog.com/res/ad76d46b-2a83-4600-bbe7-10d91df6ed6d.jpg',
						'https://static.88gog.com/res/388ebd80-7084-4d6c-9dfc-d5ff71721ffc.jpg',
						'https://static.88gog.com/res/50b325f5-7ff6-46df-97f0-97a90c6fe63c.jpg',
					]
				],
				show: true,
				evaluateArr: [{
						user_info: {
							name: "小小池塘边儿",
							active: '../../static/user.png',
							is_vip: true,
						},
						date: '01-24',
						content: '艾露猫，从船撞坏的那一刻起就一只陪伴着我，从第一只大贼龙到冥灯龙，从冰鱼龙到最后的黑龙，猫猫看着我从一个什么都不懂的菜鸟猎人逐渐成长为一个能单刷F4的苍蓝星。猎人在龙面前已经足够渺小，而更加渺小的猫猫却承受了不该是这个体型承受的伤害，还能在空闲之余做各种各样的事，从一开始的蜜虫猫猫专职奶妈，几次救我与危难之中，到后面带上掠夺刀与资本家猎人一起榨干每一条龙，带上大盾吸引仇恨，带上笛子肆意吹buff，那段时光，或许是艾露猫最快乐的时光吧，与猎人一起面对体型巨大的怪物，一起采素材，一起做更好的装备一步步成长，猎人学会了各种各样的技能，猫猫也获得了不同的装备道具',
						images: [
							'../../static/20240514215946_1.jpg',
							'../../static/20240514215951_1.jpg',
							'../../static/20240523171238_1.jpg',
						],
						score: 5,
						comment: 1086,
						like: 1086,
						click: false
					},
					{
						user_info: {
							name: "天暗星",
							active: '../../static/user.png',
							is_vip: true,
						},
						date: '01-24',
						content: '带阿白入坑的时候，我已经是千场太刀侠了他对于太刀的居合斩和登龙很眼馋，所以也选择太刀开荒。确实是一种别样的体验，我喝着大回复药，演奏笛子，偶尔输出下，看着这个还没成长起来的太刀侠的登龙空了，被各种爪子，尾巴，尖刺，吐息一下打飞。我一边幸灾乐祸一边给他回血，不过阿白就像他自己说的那样--是个有“太刀之魂”的猎人。',
						images: [
							'../../static/20240514215946_1.jpg',
							'../../static/20240514215951_1.jpg',
							'../../static/20240523171238_1.jpg',
						],
						score: 4,
						comment: 46,
						like: 80,
						click: false
					},
					{
						user_info: {
							name: "天暗星",
							active: '../../static/user.png',
							is_vip: false
						},
						date: '01-24',
						content: '当初玩这个游戏的契机很离谱:我以前养了一只暹罗猫，知道这个游戏里也有暹罗猫后就买了，给游戏里的随从猫起了和我现实中的猫一样的名字。20年的时候我的猫去世了，我也基本上不玩怪猎了不过我偶尔还是会上游戏看几眼，因为我真的很想我的猫，每当我看到游戏里的那只同名的暹罗猫坐在屋子的角落，我会骗自己我的猫还活着，他只是去了一个充满未知和冒险的世界陪伴我而已。',
						images: [
							'../../static/20240514215946_1.jpg',
							'../../static/20240514215951_1.jpg',
							'../../static/20240523171238_1.jpg',
						],
						score: 4,
						comment: 47,
						like: 23,
						click: false
					}
				]
			})

			// 点赞
			const like_click = (e: any) => {
				e.click = !e.click;
				e.like += e.click ? 1 : -1;
			}

			// 查看图片
			const click_img = (index: number, images: Array) => {
				uni.previewImage({
					urls: images,
					current: index
				})
			}

			// 监听滚动 并节流 隐藏
			const handleScroll = () => {
				if (gamesRef.value) {
					showTOP.value = gamesRef.value.scrollTop > TOP ? true : false;
					if (debounceTimer) {
						clearTimeout(debounceTimer);
					}
					debounceTimer = setTimeout(() => {
						showTOP.value = false;
					}, 1500);
				}
			};


			const scrollToTop = () => {
				if (gamesRef.value) {
					gamesRef.value.scrollTop = 0;
				}
			};


			const showToastF = (title: string) => {
				uni.showToast({
					title,
					icon: 'none'
				})
			}

			onMounted(() => {
				gamesRef.value.addEventListener('scroll', handleScroll);
			});
			onBeforeUnmount(() => {
				if (gamesRef.value) {
					gamesRef.value.removeEventListener('scroll', handleScroll);

				}
				if (debounceTimer) {
					clearTimeout(debounceTimer);
				}
			});


			return {
				...toRefs(state),
				like_click,
				click_img,
				gamesRef,
				showTOP,
				scrollToTop,
				showModal,
				showToastF
			}

		},
		onLoad(options: {
			[key: string]: any
		}) {
			if (options.type && options.type == 1) {
				this.type = options.type;

			}
			if (options.id && options.id == 1) {
				this.id = options.id;
			}
		}
	}
</script>

<style lang="scss">
	page {
		font-family: PingFang SC, PingFang SC;
		box-sizing: border-box;
	}

	.games {
		height: 100vh;
		// width: 100vh;
		// position: relative;
		overflow: hidden;
		overflow-y: scroll;
		scroll-behavior: smooth;

		.img_bg {
			position: absolute;
			top: 0;
			right: 0;
			bottom: 0;
			left: 0;
		
			filter: blur(50rpx);
			z-index: -1;
		}

		&::after {
			content: "";
			position: absolute;
			top: 0;
			right: 0;
			bottom: 0;
			left: 0;
			background: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5));
			z-index: 0;
		}


	}


	.content {
		position: relative;
		z-index: 1;
		color: white;
		width: 100vw;
	}

	.nav {
		width: 100%;
		position: fixed;
		z-index: 999;
		left: 0;
		top: 0;
	}

	.score-box {
		width: 160rpx;
		height: 160rpx;
		background: url('../../static/score.png') no-repeat center center/cover;
	}

	.flipped-image {
		transform: rotateY(180deg);
		-webkit-transform: rotateY(180deg);
	}

	.tabs {
		overflow: hidden;
		margin-top: 25rpx;

		.tab {
			float: left;
			background: url('../../static/line.png') no-repeat center center/cover;
			border: 1rpx solid #ccc;
			padding: 10rpx 20rpx;
			margin-top: 15rpx;
			margin-right: 15rpx;
		}
	}

	// 轮播图
	.banner-container {
		width: 100%;
		height: 400rpx;
	}
	@media (min-width: 1200px) {
	    .banner-container {
	        height: 700rpx;
	    }
	}
	


	.banner-item {
		display: flex;
		justify-content: center;
	}

	.banner-box {
		width: 99%;
		height: 100%;
		padding: 0 5rpx;
	}

	.banner-img {
		width: 100%;
		height: 100%;
		border-radius: 25rpx;
	}




	.button-game {
		width: 100%;
		height: 80rpx;
		background: url('../../static/button.png') no-repeat center center/cover;
	}

	.swiper-box {
		position: relative;
	}

	.swiper-bg {
		position: absolute;
		z-index: 9;
		right: 62rpx;
		top: -28rpx;
		height: 80rpx;

		// background: url('../../static/swiper-bg.png') no-repeat center center/contain;
		.text-box {
			padding: 0 100rpx 0 20rpx;
			margin-top: -80rpx;
			position: relative;
			z-index: 10;
		}
	}

	// 正在玩人数动画
	@keyframes fadeOut {
		from {
			opacity: 1;
		}

		to {
			opacity: 0;
		}
	}

	@keyframes fadeIn {
		from {
			opacity: 0;
		}

		to {
			opacity: 1;
		}
	}

	.hide {
		animation: fadeOut 0.5s forwards;
	}

	.show {
		animation: fadeIn 0.5s forwards;
	}
	.content-img{
		height: 150rpx;
	}
	 
	
	@media (min-width: 1200px) {
	   .content-img{
	   	height: 450rpx;
	   }
	}
	.Version {
		background: rgba(245, 246, 250, 0.1);
		border-radius: 44rpx;

		&.Version-else {
			height: 88rpx;

			.justify-center {
				&:last-child {
					position: relative;

					&::before {
						content: '';
						height: 24rpx;
						border-left: 1rpx solid #F5F6FA;
						position: absolute;
						left: 0;
						top: 50%;
						transform: translateY(-50%);
					}
				}
			}
		}
	}



	.download {
		height: 100rpx;
		background: url('../../static/download.png')no-repeat center center/cover;

		.text-gray {
			font-size: 18rpx;
		}
	}


	.button2 {
		height: 100rpx;
		background: url('../../static/button2.png')no-repeat center center/cover;
	}



	.date {
		font-weight: 400;
		font-size: 22rpx;
		color: #626266;
		line-height: 0px;
		text-align: left;
		font-style: normal;
		text-transform: none;
	}

	.score_box {
		image {
			width: 36rpx;
			height: 36rpx;
			margin-right: 5rpx;
		}
	}

	.back_to_top {
		position: fixed;
		right: 40rpx;
		bottom: 100rpx;
		z-index: 989;

		view {
			width: 72rpx;
			height: 72rpx;
			padding: 10rpx;
			border-radius: 50%;
			background-color: #777781;
		}
	}

	// 点赞动画
	.rotateScale_init {
		animation: rotateScale 1s forwards;
	}

	@keyframes rotateScale {
		0% {
			transform: rotate(0deg) scale(1);
		}

		50% {
			transform: rotate(-10deg) scale(1.3);
		}

		100% {
			transform: rotate(0deg) scale(1);
		}
	}

	.modal-box {
		position: relative;
	}

	.modal {
		opacity: 0;
		position: absolute;
		top: 35rpx;
		left: -32vw;
		width: calc(100vw - 20rpx);
		background: rgba(0, 0, 0, .8);
		border-radius: 1.6vw;
		backdrop-filter: blur(1.333333vw);
		z-index: 10;
	}
</style>
