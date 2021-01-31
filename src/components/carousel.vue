<template>
  <div class="project-pic">
    <img class="display-pic" v-if="screenSize > 768" :src="projectImage[picSelector]" alt="">
    <div class="control">
      <h2>Preview</h2>
      <div class="arrow-box">
        <button @click.prevent="scrollLeft"><left-arrow :fillColor="iconColor"/></button>
        <button @click.prevent="scrollRight"><right-arrow :fillColor="iconColor"/></button>
      </div>
    </div>
    <div class="pic-carousel" ref="carousel">
      <div class="col-md-4" v-for="(item, index) in projectImage" :key="item">
        <img class="carousel-pic" :src="item" alt="" @click="choosePic(index)">
      </div>
    </div>
  </div>
</template>

<script>
import leftArrow from 'vue-material-design-icons/ChevronLeft.vue'
import rightArrow from 'vue-material-design-icons/ChevronRight.vue'
export default {
  components: {
    leftArrow,
    rightArrow
  },
  props: {
    projectImage: {
      type: Array,
      required: true
    }
  },
  data: () => ({
    screenSize: '',
    picSelector: 0,
    iconColor: '#0000006e'
  }),
  methods: {
    choosePic (i) {
      this.picSelector = i
    },
    scrollLeft () {
      const carouselContainer = this.$refs.carousel
      const scroll = carouselContainer.scrollLeft - (carouselContainer.lastElementChild.offsetWidth)
      const width = carouselContainer.lastElementChild.offsetWidth
      const scrollTo = scroll === -width ? 30000 : scroll
      console.log('scroll' + scroll)
      console.log('width' + width)
      carouselContainer.scrollTo({
        left: scrollTo,
        behavior: 'smooth'
      })
    },
    scrollRight () {
      const carouselContainer = this.$refs.carousel
      const cardsNumber = carouselContainer.children.length
      const scroll = carouselContainer.scrollLeft + (carouselContainer.lastElementChild.offsetWidth)
      const width = carouselContainer.lastElementChild.offsetWidth
      const totalWidth = width * cardsNumber
      const sizemultiple = this.screenSize < 768 ? 1 : 2
      console.log(sizemultiple)
      console.log('scroll' + scroll)
      console.log('width' + width)
      console.log('totalWidth' + totalWidth)
      if (sizemultiple === 1) {
        const scrollTo = scroll * sizemultiple + cardsNumber > totalWidth ? -width : scroll
        carouselContainer.scrollTo({
          left: scrollTo,
          behavior: 'smooth'
        })
      } else {
        const scrollTo = scroll * sizemultiple > totalWidth ? -width : scroll
        carouselContainer.scrollTo({
          left: scrollTo,
          behavior: 'smooth'
        })
      }
    },
    resizeHandle () {
      this.screenSize = window.screen.availWidth
    }
  },
  created () {
    window.addEventListener('resize', this.resizeHandle)
    this.resizeHandle()
  },
  destroyed () {
    window.addEventListener('resize', this.resizeHandle)
  }
}
</script>

<style lang="scss" scoped>
.project-pic{
  padding: 10px 0;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  img{
    width: 100%;
    align-self: center;
    border-radius: 10px;
    cursor: pointer;
  }
  .control{
    display: flex;
    justify-content: space-between;
    .arrow-box{
      display: flex;
    }
  }
  h2{
    font-size: 1.5rem;
    font-weight: 600;
    @media (max-width: 768px) {
      font-size: 1rem;
      font-weight: bolder;
    }
  }
  .pic-carousel{
    display: flex;
    overflow: hidden;
    flex-direction: row;
    flex-wrap: nowrap;
    width: 100%;
    .col-md-4{
      overflow: hidden;
      padding: 0;
      img{
        padding: 5px;
      }
      &::before{
        content: ' ';
        background-color: #ffffff80;
        width: 50px;
        height: 100%;
        position: absolute;
        left: 0;
        top: 0;
        z-index: 2;
        transform: skew(45deg) translateX(1000%);
        transition: transform 0.5s ease;
      }
      &:hover{
        box-shadow: inset 0px 0px 1px 1px #ffffff80;
        &::before{
          transform: skew(45deg) translateX(-220%);
        }
      }
    }
    @media (max-width: 768px) {
      overflow: auto;
    }
    .col-md-4{
      @media (max-width: 768px) {
        flex: 0 0 100%;
        display: flex;
        justify-content: center;
        img{
          width: 100%;
        }
        &::before{
          transform: skew(45deg) translateX(1574%);
        }
        &:hover{
          box-shadow: inset 0px 0px 1px 1px #ffffff80;
          &::before{
            transform: skew(45deg) translateX(-320%);
          }
        }
      }
    }
  }
}
</style>
