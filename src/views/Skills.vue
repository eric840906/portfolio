<template>
  <div class="skills">
    <div class="col-md-6" v-for="item in skills" :key="item.title">
      <div class="skill-card">
        <h1>{{item.title}}</h1>
        <div class="skill-tags">
          <div class="col-4" v-for="tag in item.tags" :key="tag.name">
            <div class="skill-tag">
              <div class="icon" :class="tag.icon"></div>
              <p>{{tag.name}}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { gsap } from 'gsap'
export default {
  data: () => ({
    skills: [
      {
        title: 'Frontend',
        tags: [
          {
            name: 'Javascript',
            icon: 'javascript-icon'
          },
          {
            name: 'HTML',
            icon: 'html-icon'
          },
          {
            name: 'CSS',
            icon: 'css-icon'
          },
          {
            name: 'Bootstrap',
            icon: 'bootstrap-icon'
          },
          {
            name: 'JQuery',
            icon: 'jquery-icon'
          },
          {
            name: 'Scss',
            icon: 'sass-icon'
          },
          {
            name: 'Vue.js',
            icon: 'vue-icon'
          }
        ]
      },
      {
        title: 'Backend',
        tags: [
          {
            name: 'Nodejs',
            icon: 'nodejs-icon'
          },
          {
            name: 'Mongodb',
            icon: 'mongodb-icon'
          },
          {
            name: 'Express',
            icon: 'express-icon'
          }
        ]
      },
      {
        title: 'Dev tools',
        tags: [
          {
            name: 'VSCode',
            icon: 'vscode-icon'
          },
          {
            name: 'Git',
            icon: 'git-icon'
          }
        ]
      },
      {
        title: 'Design tools',
        tags: [
          {
            name: 'Affinity photo',
            icon: 'affinity-icon'
          },
          {
            name: 'Figma',
            icon: 'figma-icon'
          }
        ]
      }
    ]
  }),
  mounted () {
    gsap.from('.skill-tag', { duration: 1, y: 'random(-100%, 100%)', opacity: 0, stagger: 0.33 })
    gsap.from('.skill-card h1', { opacity: 0, stagger: 0.33 })
  }
}
</script>

<style lang="scss" scoped>
@import '@/assets/style/scss/mixin.scss';
@import '@/assets/style/scss/icon.scss';
.skills{
  @include router-theme(row, center, flex-start);
  position: fixed;
  width: 100%;
  flex-wrap: wrap;
  padding: 20px;
  .skill-card{
    display: flex;
    flex-direction: column;
    min-height: 300px;
    h1{
      font-weight: bolder;
    }
    .skill-tags{
      display: flex;
      flex-wrap: wrap;
      .skill-tag{
        font-weight: 500;
        display: flex;
        flex-direction: column;
        align-items: center;
        margin-top: 30%;
        .icon{
          height: 30px;
        }
      }
    }
  }
}
</style>
