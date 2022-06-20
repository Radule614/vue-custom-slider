<script>
import SlideContent from './SlideContent.vue';
export default{
  components:{
    SlideContent
  },
  props:['item-array'],
  data(){
    return{
      sliderPosition: 0,
      sliderLastPossiblePosition: 0,
      sliderViewport: 0,
      
      slideWidth: 0,
      slideHeight: 0,
      slideSpacing: 0,
      slideNumber: 3,
    
      currentSlide: 0
    }
  },
  mounted(){
    this.calculateDimensions();
    this.resizeHandler();
    window.addEventListener('resize', this.resizeHandler);
  },
  unmounted() {
    window.removeEventListener('resize', this.resizeHandler);
  },
  methods: {
    resizeHandler() {
      if(this.itemArray && this.itemArray.length > 0){
        this.slideNumber = parseInt(window.innerWidth / this.slideWidth - 0.7);
        this.calculateDimensions();
      }
    },
    calculateDimensions(){
      if(this.itemArray && this.itemArray.length > 0){
        let slide = this.$refs.slideEl[0];
        this.slideWidth = slide.clientWidth;
        this.slideHeight = slide.clientHeight;
        this.slideSpacing = 2*parseFloat((slide.currentStyle || window.getComputedStyle(slide)).marginRight);
        this.sliderViewport= this.slideNumber * (this.slideWidth + this.slideSpacing) - this.slideSpacing;
        this.sliderLastPossiblePosition = (this.itemArray.length - this.slideNumber) * (this.slideWidth + this.slideSpacing);
        this.calculateCurrentSlide();
      }
    },
    goForward(){
      if(this.sliderPosition <= -this.sliderLastPossiblePosition){
        this.sliderPosition = 0;
      }else{
        this.sliderPosition -= this.slideWidth + this.slideSpacing;
      }
      this.calculateCurrentSlide();
    },
    goBackward(){
      if(this.sliderPosition >= 0){
        this.sliderPosition = -this.sliderLastPossiblePosition;
      }else{
        this.sliderPosition += this.slideWidth + this.slideSpacing;
      }
      this.calculateCurrentSlide();
    },
    calculateCurrentSlide(){
      this.currentSlide = Math.abs(this.sliderPosition)/(this.slideWidth+this.slideSpacing);
    }
  }
}
</script>

<template>
  <div class="slider-container">
    <div class="slider-wrap">
      <div class="arrow-left" @click="goBackward"></div>
      <div class="slider-inner" ref="sliderInnerEl" :style="{'width': sliderViewport + 'px', 'height': slideHeight + 'px'}">
        <div class="slider" :style="{'transform': `translateX(${sliderPosition}px)`}">
          <div class="slide"  ref="slideEl" v-for="(item, index) in itemArray" :key="index">
            <slide-content :item="item"></slide-content>
          </div>
        </div>
      </div>
      <div class="arrow-right" @click="goForward"></div>
    </div>
  </div>
</template>

<style scoped>
.slider-container{
  position: relative;
}

.slider-wrap{
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
}
.slider-inner{
  position: relative;
  
  overflow-x:hidden;
  padding:10px;
}
.slider{
  overflow-x: hidden;
  position: absolute;
  top:0px;
  left:0px;
  display: flex;
  padding:10px;
  transition: transform 0.4s ease-out;
}

.slider > .slide{
  margin:0px 15px; /* slide spacing */
  box-shadow: 0px 0px 5px rgba(0, 0, 0, 0.3);
}

.slider > .slide:first-child{
  margin-left:0px;
}

.arrow-left,
.arrow-right{
  position: relative;
  width: 0;
  height: 0;
  border-style: solid;
  cursor: pointer;
}

.arrow-left{
  margin-right: 10px;
  border-width: 28px 22px 28px 0; /* left arrow size */
  border-color: transparent #555 transparent transparent;
}

.arrow-right{
  margin-left: 10px;
  border-width: 28px 0 28px 22px; /* right arrow size */
  border-color: transparent transparent transparent #555;
}

.arrow-left:hover{
  border-color: transparent #000 transparent transparent;
}
.arrow-right:hover{
  border-color: transparent transparent transparent #000;
}

</style>