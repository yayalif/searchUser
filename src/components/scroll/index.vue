<template>
<div class="contaniner">
<div id="header">iScroll</div>
<div id="wrapper">
	<div id="scroller">
		<ul>
			<li>Pretty cell 1</li>
			<li>Pretty cell 2</li>
			<li>Pretty cell 3</li>
			<li>Pretty cell 4</li>
			<li>Pretty cell 5</li>
			<li>Pretty cell 6</li>
			<li>Pretty cell 7</li>
			<li>Pretty cell 8</li>
			<li>Pretty cell 9</li>
			<li>Pretty cell 10</li>
			<li>Pretty cell 11</li>
			<li>Pretty cell 12</li>
			<li>Pretty cell 13</li>
			<li>Pretty cell 14</li>
			<li>Pretty cell 15</li>
			<li>Pretty cell 16</li>
			<li>Pretty cell 17</li>
			<li>Pretty cell 18</li>
			<li>Pretty cell 19</li>
			<li>Pretty cell 20</li>
		</ul>
	</div>
</div>
<div class="verticalWrapper" @touchmove="scrollMove">
	<div class="verticalScroll">
		<ul class="refresh">
			<li v-if="loading === 1" class="refresh-li">下拉加载...</li>
			<li v-if="loading === 2" class="refresh-li">松开刷新...</li>
		</ul>
			<div :class="getItemWrapper(index)" v-for="(item, index) in 30" :key="index" @touchmove="scrollItem">
				<div class="opt-scroll">
						<div class="opt-items">
							<div class="content">
								<div class="info">
									<span class="name">浩浩荡荡</span>
									<span class="time"></span>
								</div>
								<div class="value">今天是个好天气，很好的天气</div>
							</div>
							<div class="opt">
								<div class="read">标未读</div>
								<div class="del">删除</div>
							</div>
						</div>
				</div>
			</div>
</div>

</div>
</div>
</template>
<script>
import  "./iscroll-probe";
export default {
	data() {
		return {
			// 垂直滚动
			vScroll: null,
			// 下拉刷新
			loading: 1,
			// 是否触发更新
			refresh: false,
			// 是否显示下拉刷新
			showRefresh: false,
			iScrollList: []

		}
	},
	mounted () {
		var myScroll;
		myScroll = new IScroll('#wrapper', {
							eventPassthrough: true, 
							scrollX: true, 
							scrollY: false,
							preventDefault: false });
			// 横向滚动
			this.optInit()

			// 垂直滚动
			this.vScroll = new IScroll('.verticalWrapper', {
										scrollX: false, 
										scrollY: true,
										preventDefault: false 
										});
			this.vScroll.on('touchmove', () => {
				// 不生效
				// if (this.vScroll.distY > 30 && this.vScroll.distY < 100 && this.vScroll.directionY < 0) {
				// 	// 说明向下拉
				// 	this.loading = 1
				// } else if (this.vScroll.distY > 100 && this.vScroll.directionY < 0) {
				// 	// 拉到最大位置
				// 	this.loading = 2
				// }
			})
			this.vScroll.on('scrollEnd', () => {
				this.showRefresh = false
			})
	},
	methods: {
		getItemWrapper (i) {
			return 'opt-wrapper' + i
		},
		optInit () {
			for (let i = 0; i < 30; i++) {
				this.iScrollList[i] = new IScroll('.opt-wrapper'+ i, {
					eventPassthrough: true, 
					scrollX: true, 
					scrollY: false,
					bounce: false,
					preventDefault: false,
					mouseWheel: true
				});
			}
		},
		/**
		 * 监听 verticalWrapper 滚动事件
		 */
		scrollMove () {
			if (this.vScroll.distY > 30 && this.vScroll.distY < 100 && this.vScroll.directionY < 0) {
				// 说明向下拉
				this.loading = 1
			} else if (this.vScroll.distY > 100 && this.vScroll.directionY < 0) {
				// 拉到最大位置
				this.loading = 2
			}
			// item 恢复原位
		},
		/**
		 * 监听 verticalWrapper 滚动事件
		 */
		scrollItem () {
		}
	}
}
</script>>

<style>
* {
	-webkit-box-sizing: border-box;
	-moz-box-sizing: border-box;
	box-sizing: border-box;
}
body,ul,li {
	padding: 0;
	margin: 0;
	border: 0;
}

body {
	font-size: 12px;
	font-family: ubuntu, helvetica, arial;
}

#header {
	width: 100%;
	height: 45px;
	line-height: 45px;
	background: #CD235C;
	padding: 0;
	color: #eee;
	font-size: 20px;
	text-align: center;
	font-weight: bold;
}

#wrapper {
	position: relative;
	z-index: 1;
	height: 160px;
	width: 100%;
	background: #ccc;
	overflow: hidden;
	-ms-touch-action: none;
}

#scroller {
	position: relative;
	z-index: 1;
	-webkit-tap-highlight-color: rgba(0,0,0,0);
	width: 2400px;
	height: 160px;
	-webkit-transform: translateZ(0);
	-moz-transform: translateZ(0);
	-ms-transform: translateZ(0);
	-o-transform: translateZ(0);
	transform: translateZ(0);
	-webkit-touch-callout: none;
	-webkit-user-select: none;
	-moz-user-select: none;
	-ms-user-select: none;
	user-select: none;
	-webkit-text-size-adjust: none;
	-moz-text-size-adjust: none;
	-ms-text-size-adjust: none;
	-o-text-size-adjust: none;
	text-size-adjust: none;
}

#scroller ul {
	list-style: none;
	width: 100%;
	padding: 0;
	margin: 0;
}

#scroller li {
	width: 120px;
	height: 160px;
	float: left;
	line-height: 160px;
	border-right: 1px solid #ccc;
	border-bottom: 1px solid #ccc;
	background-color: #fafafa;
	font-size: 14px;
	overflow: hidden;
	text-align: center;
}

p {
	font-size: 16px;
	padding: 1.2em;
	line-height: 200%;
}
.verticalWrapper {
	width: 100%;
	height: 500px;
	overflow: scroll;
}
.refresh li{
	/* opacity: 1;
	transition: all .5s linear; */
	text-align: center;
}
.verticalScroll {
	width: 100%;
	height: 2440px;
	position: relative;
	top: -16px;
}
.opt-wrapper {
	position: relative;
	z-index: 1;
	/* height: 80px; */
	width: 100%;
	background: #ccc;
	overflow: hidden;
	-ms-touch-action: none;
}
.opt-scroll {
	position: relative;
	z-index: 1;
	-webkit-tap-highlight-color: rgba(0,0,0,0);
	width: 140vw;
	/* height: 80px; */
	-webkit-transform: translateZ(0);
	-moz-transform: translateZ(0);
	-ms-transform: translateZ(0);
	-o-transform: translateZ(0);
	transform: translateZ(0);
	-webkit-touch-callout: none;
	-webkit-user-select: none;
	-moz-user-select: none;
	-ms-user-select: none;
	user-select: none;
	-webkit-text-size-adjust: none;
	-moz-text-size-adjust: none;
	-ms-text-size-adjust: none;
	-o-text-size-adjust: none;
	text-size-adjust: none;
}
.opt-items {
	width: 100%;
	display:flex;
	justify-items: center;
	white-space: nowrap;
	flex-wrap: nowrap;
	border-bottom: 1px solid #999;
}
.content {
	/* flex-grow: 1; */
	width: 100vw;
	height: 100%;
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
	background-color: #fff;
}
.info {
	width: 100%;
	height: 50%;
	line-height: 40px;
	text-align: center;
}
.value {
	height: 50%;
	line-height: 40px;
	text-align: center;
}
.opt {
	width: 20vw;
	flex-shrink: 0;
}

.read {
	width: 20vw;
	height: 100%;
	background-color: rgb(199, 247, 247);
	display: inline-block;
	text-align: center;
	line-height: 80px;
}
.del {
	width: 20vw;
	height: 100%;
	background-color: #f00;
	line-height: 80px;
	text-align: center;
	display: inline-block;
}
</style>