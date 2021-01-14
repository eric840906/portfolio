<template>
  <div class="projects">
    <div class="project-selector">
      <div class="indicator" v-for="(item, index) in project" :key="index" @click="projectSelector = index" :class="{'active': projectSelector === index }"></div>
    </div>
    <div class="col-md-4">
      <div class="project-info">
        <h1 class="project-name">
          {{project[projectSelector].name}}
        </h1>
        <div class="project-skill">
          <h2>Used tech</h2>
          <div class="project-tags">
            <span class="project-tag" :class="tag.icon" v-for="tag in project[projectSelector].tags" :key="tag.name">
              {{tag.name}}
            </span>
            <!-- <span class="project-tag vue-icon"></span>
            <span class="project-tag jquery-icon"></span>
            <span class="project-tag bootstrap-icon"></span> -->
          </div>
        </div>
        <div class="project-desc">
          <h2>Description</h2>
          <p>{{project[projectSelector].desc}}</p>
        </div>
        <div class="btn-box">
          <a :href="project[projectSelector].links.repo">Repo</a>
          <a :href="project[projectSelector].links.demo">Demo</a>
        </div>
      </div>
    </div>
    <div class="col-md-8">
      <carousel :projectImage='project[projectSelector].image'></carousel>
    </div>
  </div>
</template>

<script>
import carousel from '@/components/carousel.vue'
export default {
  components: {
    carousel
  },
  data: () => ({
    projectSelector: 0,
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
        image: [require('../assets/image/Lac1.png'), require('../assets/image/Lac2.png'), require('../assets/image/Lac3.png'), require('../assets/image/Lac4.png'), require('../assets/image/Lac5.png'), require('../assets/image/Lac6.png')]
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
        image: [require('../assets/image/wh1.png'), require('../assets/image/wh2.png'), require('../assets/image/wh3.png'), require('../assets/image/wh4.png'), require('../assets/image/wh5.png'), require('../assets/image/wh6.png')]
      }
    ]
  }),
  methods: {
    changeSelector (i) {
      this.projectSelector = (this.projectSelector + this.project.length + i) % this.project.length
    }
  },
  mounted () {
    window.addEventListener('wheel', (e) => {
      const scroll = e.deltaY === -100 ? this.changeSelector(-1) : this.changeSelector(1)
      return scroll
    })
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
  }
  .btn-box{
    display: flex;
    justify-content: space-around;
    margin-top: 80px;
    border-top: 1px solid #ffffff54;
    margin-top: auto;
    a{
      display: inline-block;
      padding: 10px;
      font-size: 24px;
      color: #2830ba8f;
      width: 50%;
      text-align: center;
      transition: 0.3s ease all;
      font-weight: bolder;
      &:hover{
        color: #ffffffad;
        background: #00000038;
        box-shadow: inset 0 0px 14px 2px #ffffff87;
      }
    }
  }
  .project-info{
    border-right: 1px solid #ffffff54;
    height: 100%;
    display: flex;
    flex-direction: column;
  }
  .project-desc{
    border-top: 1px solid #ffffff54;
    padding-top: 2.5em;
    display: flex;
    flex-direction: column;
    p{
      width: 80%;
    }
  }
  .project-skill{
    border-top: 1px solid #ffffff54;
    padding-top: 2em;
    margin-bottom: 10em;
  }
  .project-tags{
    .project-tag+.project-tag{
      margin-left: 30px;
    }
    .project-tag{
      width: 25px;
    }
  }
  .project-selector{
    position: absolute;
    left: 5px;
    top: 50%;
    transform: translateY(-50%);
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
