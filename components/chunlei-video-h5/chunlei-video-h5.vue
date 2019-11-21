<template>
	<view>
		<video show-fullscreen-btn show-progress enable-progress-gesture
			:direction="direction" :src="src" :loop="loop" @play="playing"
			id="chunleiVideo" ref="chunleiVideo" class="video">
		</video>
	</view>
</template>

<script>
	export default{ 
		props:{
			src:{
				type:String,
				default:''
			},
			play:{
				type:Boolean,
				default:false
			}
		},
		data(){
			return{
				time:0,
				direction:-90,
				loop:false,
				playFirst:true
			}
		},
		mounted() {
			this.videoCtx = uni.createVideoContext(`chunleiVideo`,this)
			
		},
		methods:{
			videoPlay(){
				if(!this.play){
					this.videoCtx.play();
					if(this.playFirst){
						this.videoCtx.seek(this.initialTime)
						this.playFirst = false
					} 
				}else{
					this.videoCtx.pause();
				}
				this.play = !this.play
			},
			waiting(){
				
			}
		},
		watch:{
			play(newVal,oldVal){
				this.videoPlay()
			},
		},
		computed:{
		}
	}
</script>

<style scoped>
	.video{
		height: 200px;
		width: 750rpx;
	}
</style>
