<template>
  <div class="projects">
    <div class="project-selector">
      <div class="indicator" v-for="(item, index) in project" :key="index" @click="projectSelector = index" :class="{'active': projectSelector === index }"></div>
    </div>
    <div class="col-md-4">
      <div class="project-info">
        <h1 class="project-name">
         <span v-for="(word,index) in splitTitle" :key="index" ref="splitText">{{word}}</span>
        </h1>
        <div class="project-skill">
          <h2>Tech</h2>
          <div class="project-tags">
            <span class="project-tag" ref="tag" :class="tag.icon" v-for="tag in project[projectSelector].tags" :key="tag.name">
              {{tag.name}}
            </span>
          </div>
        </div>
        <div class="project-desc">
          <h2>Description</h2>
          <p><span v-for="(word,index) in splitDesc" :key="index" ref="splitDesc">{{word}}</span></p>
        </div>
        <div class="btn-box">
          <a target="blank" :href="project[projectSelector].links.repo">Repo</a>
          <a target="blank" :href="project[projectSelector].links.demo">Demo</a>
        </div>
      </div>
    </div>
    <div class="col-md-8">
      <carousel :projectImage='project[projectSelector].image'></carousel>
    </div>
  </div>
</template>

<script>
import { gsap } from 'gsap'
import carousel from '@/components/carousel.vue'
export default {
  components: {
    carousel
  },
  data: () => ({
    projectSelector: 0,
    screenSize: undefined,
    project: [
      {
        name: 'Lächeln',
        tags: [
          {
            name: 'Vue.js',
            icon: 'vue-icon'
          },
          {
            name: 'JQuery',
            icon: 'jquery-icon'
          },
          {
            name: 'Bootstrap',
            icon: 'bootstrap-icon'
          }
        ],
        desc: '購物車及商品部份是使用六角學院免費提供的api，前端切版部份則由自己動手、有使用leaflet的地圖套件功能，大部分的slider使用vue製作以達成可重複利用效果',
        links: {
          repo: 'https://github.com/eric840906/vuecli3Project1',
          demo: 'https://eric840906.github.io/vuecli3Project1/#/home'
        },
        image: ['https://imgur.com/hik8jMn.png', 'https://imgur.com/KcjvIIs.png', 'https://imgur.com/IBeISrh.png', 'https://imgur.com/0lQaUGa.png', 'https://imgur.com/yC9JGlz.png', 'https://imgur.com/eNu9eBZ.png']
      },
      {
        name: 'Whelper',
        tags: [
          {
            name: 'Vue.js',
            icon: 'vue-icon'
          },
          {
            name: 'Nodejs',
            icon: 'nodejs-icon'
          },
          {
            name: 'Express',
            icon: 'express-icon'
          },
          {
            name: 'Mongodb',
            icon: 'mongodb-icon'
          },
          {
            name: 'Bootstrap',
            icon: 'bootstrap-icon'
          }
        ],
        desc: '以自己日常生活會用到的東西為發想製作的web app，主要用途是規劃每日菜單及分析營養攝取，前後端全部由自己負責，前端使用vue、後端使用nodejs，還有製作使用者登入及大頭貼裁切等功能，可使用帳號publictest@gmail.com，密碼publictest來試用',
        links: {
          repo: 'https://github.com/eric840906/WeightHelper',
          demo: 'https://eric840906.github.io/WeightHelper/'
        },
        image: ['https://imgur.com/18CtN7H.png', 'https://imgur.com/M7IrVge.png', 'https://imgur.com/ro20XSa.png', 'https://imgur.com/54CnE4P.png', 'https://imgur.com/0LmnSFK.png', 'https://imgur.com/M7UvICE.png']
      },
      {
        name: 'Dashboard',
        tags: [
          {
            name: 'Vue.js',
            icon: 'vue-icon'
          },
          {
            name: 'Bootstrap',
            icon: 'bootstrap-icon'
          }
        ],
        desc: 'Dashboard切版練習，主要練習自訂義chartjs的應用，有用到vue的custom directive功能製作右上角使用者功能列',
        links: {
          repo: 'https://github.com/eric840906/dashboardPractice',
          demo: 'https://eric840906.github.io/dashboardPractice/#/login'
        },
        image: ['https://imgur.com/5KFwEpm.png', 'https://imgur.com/UQQhSHd.png', 'https://imgur.com/Zt6os4l.png']
      }
    ]
  }),
  methods: {
    changeSelector (i) {
      this.projectSelector = (this.projectSelector + this.project.length + i) % this.project.length
    },
    resizeHandle () {
      this.screenSize = window.screen.availWidth
    }
  },
  updated () {
    const tl = gsap.timeline()
    gsap.from('.carousel-pic', { duration: 0.5, opacity: 0, x: -50, stagger: 0.1 })
    if (this.screenSize > 768) {
      gsap.fromTo('.display-pic', { opacity: 0, y: -50 }, { opacity: 1, y: 0, duration: 1 })
    }
    gsap.fromTo(this.$refs.tag, {
      opacity: 0,
      x: gsap.utils.random(-500, 500),
      y: gsap.utils.random(-500, 500),
      z: gsap.utils.random(-500, 500),
      rotate: 270
    }, { opacity: 1, x: 0, y: 0, z: 0, ease: 'expo', duration: 1, rotate: 0, stagger: 0.1 })
    tl.fromTo(this.$refs.splitText, {
      opacity: 0,
      x: gsap.utils.random(-500, 500),
      y: gsap.utils.random(-500, 500),
      z: gsap.utils.random(-500, 500),
      rotate: 270
    }, { opacity: 1, x: 0, y: 0, z: 0, duration: 1, rotate: 0, stagger: 0.1 })
    tl.fromTo(this.$refs.splitDesc, {
      opacity: 0,
      rotate: gsap.utils.random(180, 30),
      y: -50
    }, { opacity: 1, rotate: 0, y: 0, duration: 0.5, stagger: 0.05 }, '-=2')
  },
  // mounted () {
  //   window.addEventListener('wheel', (e) => {
  //     const scroll = e.deltaY === -100 ? this.changeSelector(-1) : this.changeSelector(1)
  //     return scroll
  //   })
  // },
  // destroyed () {
  //   window.addEventListener('wheel', (e) => {
  //     const scroll = e.deltaY === -100 ? this.changeSelector(-1) : this.changeSelector(1)
  //     return scroll
  //   })
  // },
  created () {
    this.resizeHandle()
  },
  computed: {
    splitTitle () {
      return [...this.project[this.projectSelector].name]
    },
    splitDesc () {
      return [...this.project[this.projectSelector].desc]
    }
  }
}
</script>

<style lang="scss" scoped>
@import '@/assets/style/scss/mixin.scss';
@import '@/assets/style/scss/icon.scss';
.projects{
  h2{
    font-size: 1.5rem;
    font-weight: 600;
    margin-bottom: 1em;
    @media (max-width: 768px) {
      font-size: 1rem;
      font-weight: bolder;
    }
  }
  display: flex;
  flex-wrap: wrap;
  padding: 20px;
  position: fixed;
  height: 100%;
  .project-name{
    margin: 1em 0;
    font-size: 3rem;
    font-weight: bolder;
    span{
      display: inline-block;
    }
    @media (max-width: 768px) {
      margin: 1em 0 0.5em 0;
      font-size: 1.5rem;
    }
  }
  .btn-box{
    display: flex;
    justify-content: space-around;
    margin-top: auto;
    border-top: 1px solid #ffffff54;
    @media (max-width: 768px) {
      margin-bottom: 0;
      border-bottom: 1px solid #ffffff54;
      a{
        font-size: 1rem;
      }
    }
    a{
      display: inline-block;
      position: relative;
      padding: 10px;
      font-size: 24px;
      color: #2830ba8f;
      width: 50%;
      text-align: center;
      transition: 0.3s ease all;
      font-weight: bolder;
      overflow: hidden;
      &::before{
        content: ' ';
        background-color: #ffffff80;
        width: 50px;
        height: 100%;
        position: absolute;
        left: 0;
        top: 0;
        transform: skew(45deg) translateX(330px);
        transition: transform 0.5s ease;
      }
      @media (max-width: 768px) {
        font-size: 1rem;
      }
      &:first-child{
        border-right: 1px solid #ffffff54;
      }
      &:hover{
        color: #ffffffad;
        box-shadow: inset 0px 1px 1px 1px #ffffff80;
        &::before{
          transform: skew(45deg) translateX(-150%);
        }
      }
    }
  }
  .project-info{
    border-right: 1px solid #ffffff54;
    height: 100%;
    display: flex;
    flex-direction: column;
    @media (max-width: 768px) {
      border: none;
    }
  }
  .project-desc{
    border-top: 1px solid #ffffff54;
    padding: 2em 0px;
    display: flex;
    flex-direction: column;
    p{
      width: 80%;
      span{
        display: inline-block;
      }
    }
    @media (max-width: 768px) {
      margin-bottom: 2em;
      p{
        width: 100%;
      }
    }
  }
  .project-skill{
    border-top: 1px solid #ffffff54;
    padding: 2em 0px;
    @media (max-width: 768px) {
      margin-bottom: 2em;
    }
  }
  .project-tags{
    @media (max-width: 768px) {
      display: flex;
    }
    .project-tag+.project-tag{
      margin-left: 30px;
    }
    .project-tag{
      display: inline-block;
      width: 25px;
    }
  }
  .project-selector{
    position: absolute;
    left: 5px;
    top: 50%;
    transform: translateY(-50%);
    @media (max-width: 768px) {
      left: 50%;
      top: -20px;
      transform: rotate(270deg);
    }
    .indicator+.indicator{
      margin-top: 10px;
    }
    .indicator{
      cursor: pointer;
      width: 15px;
      height: 15px;
      border-radius: 100%;
      background: #00000029;
    }
    .active{
      background: #2830ba8f;
    }
  }
}
</style>
