<template>
	<view class="box">
		<video :direction="direction" :src="src" :loop="loop" @timeupdate="timeupdate"
			:id="`video_${src}`" ref="chunleiVideo" class="video" objectFit="fill">
		</video>
		<cover-image class="img" :src="poster" v-if="poster!=''&&playFirst"></cover-image>
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
			},
			poster:{ //视频封面的图片
				type:String,
				default:''
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
			this.videoCtx = uni.createVideoContext(`video_${this.src}`,this)
			
		},
		methods:{
			timeupdate(event){
				this.time = event.detail.currentTime
			},
			videoPlay(){
				if(this.play){
					this.videoCtx.play();
					if(this.playFirst){
						this.videoCtx.seek(this.startTime)
						this.playFirst = false
					} 
				}else{
					this.videoCtx.pause();
					this.$emit('pause',this.time)
				}
			},
			waiting(){
				
			}
		},
		watch:{
			play(newVal,oldVal){
				this.videoPlay()
			},
			startTime:{
				immediate: true,
				handler(newVal,oldVal){
					this.time = newVal
				}
			}
		},
		computed:{
		}
	}
</script>

<style scoped>
	.box{
		position: relative;
	}
	.video{
		height: 200px;
		width: 750rpx;
	}
	.img{
		position: absolute;
		height: 200px;
		width: 750rpx;
	}
</style>
