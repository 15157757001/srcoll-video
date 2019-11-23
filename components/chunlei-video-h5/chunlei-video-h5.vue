<template>
	<view>
		<video :direction="direction" :src="src" :loop="loop" @timeupdate="timeupdate"
			:id="`video_${src}`" ref="chunleiVideo" class="video" objectFit="fill">
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
	.video{
		height: 200px;
		width: 750rpx;
	}
</style>
