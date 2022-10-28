<template>
  <div id="app" :style="{width:width+'px',height:height+'px'}" ref="appBox">
    <img
        src="https://p7.itc.cn/images01/20210406/90aae0d9b75b431784181aa5cd808b60.png"
    />
  </div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return {
      width:1920,
      height:1080
    }
  },
  mounted() {
    this.setScale()
    window.addEventListener('resize',this.debounce(this.setScale))
  },
  methods:{
    debounce(fn){
      let _this = this
      let timer = null;
      return function (){
        timer && clearTimeout(timer)
        timer = setTimeout(()=>{
          fn.apply(_this,arguments)
        },600)
      }
    },
    getScale(){
      let scale_width = window.innerWidth/this.width;
      let scale_height = window.innerHeight/this.height;
      return Math.min(scale_height,scale_width)
    },
    setScale() {
      let scale = this.getScale()
      this.$refs.appBox.style.transform = `scale(${scale},${scale}) translate(-50%)`
    }
  }
}
</script>

<style lang="less">
html,
body {
  position: relative;
  background: #000;
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0;

  #app {
    position: absolute;
    left: 50%;
    transform-origin: 0 0;
    transition: .3s;

    img{
      display: block;
      height: 100%;
      width: 100%;
    }
  }
}
</style>
