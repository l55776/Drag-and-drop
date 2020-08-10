<template>
	<ul class="boxes_show" id="btnball" v-on:click="show" @touchstart="touch($event)"  @touchmove="move($event)" v-bind:class="ulClass" v-bind:style="{left:L+'px',top:T+'px'}" >
		嗨
		<li v-if="dis==='s'" v-bind:style="listy1">{{text.liTxt1}}</li>
		<li v-if="dis==='s'" v-bind:style="listy2" v-on:click="licli($event)">{{text.liTxt2}}</li>
		<li v-if="dis==='s'" v-bind:style="listy3">{{text.liTxt3}}</li>
	</ul>
</template>
<!-- text代表4个球中的文本内容，ulclass是给根标签ul绑定class，可以直接在父组件中用这个class，listy1..2..3分别代表3个弹出小球的样式，需要在父组件中通过v-bind方式绑定，之后在父组件data中定义，事件我只写了第2个小球的click事件，需要的可以自己另外加，看不懂的可以联系我要引用成功的父组件代码 -->
<script>

	export default {
		data() {
			return {
				dis:'b',disX:'', disY:'', L:'', T:'', starX:'', starY:'',ballwidth:'',ballheight:'',bodywidth:'',bodyheight:''
			}
		},
		props:['dragDrop']
			
		,
		onLoad() {
		
		},
		methods: {
			licli:function(e){
				console.log(1)
				this.$emit('bbclick',this.text)
			},
			show:function(){
				if(this.dis==='b'){
					this.dis='s';
				}
				else if(this.dis==='s'){
					this.dis='b';
				}
			},
			touch:function(e){
				this.disX = e.touches[0].clientX - e.currentTarget.offsetLeft;
				this.disY = e.touches[0].clientY - e.currentTarget.offsetTop;
				this.starX = e.touches[0].clientX;
				this.starY = e.touches[0].clientY;
			}
			,
			move:function(e){
				console.log(this.dragDrop)
				this.L = e.touches[0].clientX - this.disX;
				this.T = e.touches[0].clientY - this.disY;
				var windowwidth = this.dragDrop.windowWidth;
				var windowheight = this.dragDrop.windowHeight;
				var ballwidth = 45;
				var ballheight = 45;
				var disx = windowwidth - ballwidth;
				var disy = windowheight - ballheight;
				if (this.L < 0) {
				this.L = 0;
				} else if (this.L >= disx) {
				this.L = disx;
				}//documentElement代表html页面这个元素
				if (this.T < 0) {
				this.T =22.5;
				} else if (this.T >=disy ) {
				this.T = disy;
				}
				
				
				
				
			}
	}}
</script>

<style>
*{
		padding: 0;margin: 0;
	}
	
	.boxes_show{display: flex;flex-direction: column;color: white;font-size:200%;display: flex;justify-content: center;align-items: center;position: fixed;
		top: 45vh;left: 85vw;width: 12vw;height: 12vw;
		background: rgba(0,0,0,0.5);border-radius: 50%;
	}
	
	
	.boxes_show>li{
		flex: 0 0 33%;color: white;font-size:60%;display: flex;justify-content: center;align-items: center;
	list-style: none;background: rgba(0,0,0,0.5);width: 65%;height: 65%;position: absolute;top: 0;left: 0;border-radius: 50%;
	}
	.boxes_show>li:nth-child(1){
		top: -6vh;left: -8vw;
	}
	.boxes_show>li:nth-child(2){
		top: 2vh;left: -15vw;
	}
	.boxes_show>li:nth-child(3){
		top: 10vh;left: -8vw;
	}
	
</style>
