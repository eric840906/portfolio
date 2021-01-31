<template>
  <div class="about">
    <div class="page">
      <div class="name-card">
        <img src="../assets/image/topPic.png" id="my-pic" alt="">
        <div class="social-media">
          <a class="media-icon" v-for="item in socialMedia" :href="item.link" :key="item.link">
            <component :is="item.icon"/>
          </a>
        </div>
        <h1 id="my-name">Eric Chiu</h1>
        <p id="my-position">Front-end Engineer</p>
        <a href="mailto:eric840906@hotmail.com.tw" id="my-email">
          <email-icon/>
          eric840906@hotmail.com.tw
        </a>
      </div>
    </div>
  </div>
</template>

<script>
import { gsap } from 'gsap'
import { TextPlugin } from 'gsap/TextPlugin'
import githubIcon from 'vue-material-design-icons/Github.vue'
import facebookIcon from 'vue-material-design-icons/Facebook.vue'
import linkedinIcon from 'vue-material-design-icons/Linkedin.vue'
import emailIcon from 'vue-material-design-icons/Email.vue'
export default {
  components: {
    githubIcon,
    facebookIcon,
    linkedinIcon,
    emailIcon
  },
  data: () => ({
    socialMedia: [
      {
        icon: 'githubIcon',
        link: 'https://github.com/eric840906'
      },
      {
        icon: 'facebookIcon',
        link: 'https://www.facebook.com/profile.php?id=100004245940194'
      },
      {
        icon: 'linkedinIcon',
        link: 'https://www.linkedin.com/in/eric-chiu-911a5a174/'
      }
    ]
  }),
  mounted () {
    gsap.registerPlugin(TextPlugin)
    const tl = gsap.timeline()
    tl.from('#my-pic', { duration: 1, rotation: -180, opacity: 0, scale: 0.1 })
    // tl.from('.social-media svg', { duration: 1, y: 'random(-100%, 100%)', opacity: 0, stagger: 0.33 })
    tl.from('#my-name', { duration: 1, text: '' }, '-=1')
    tl.from('#my-position', { duration: 1, text: '' })
    tl.from('#my-email', { duration: 2, text: '' }, '-=1.8')
  }
}
</script>

<style lang="scss" scoped>
@import '@/assets/style/scss/mixin.scss';
.about{
  @include router-theme(column, center, center);
  position: fixed;
  width: 100%;
}
.name-card{
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-weight: 700;

  *+*{
    margin-top: 10px;
  }
  a{
    color:#2830ba8f;
  }
  .media-icon{
    overflow: hidden;
    padding: 10px;
    display: inline-block;
    position: relative;
    .material-design-icon{
      svg{
        width: 40px;
        height: 40px;
      }
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
      transform: skew(45deg) translateX(200%);
      transition: transform 0.5s ease;
    }
    &:hover{
      box-shadow: inset 0px 0px 1px 1px #ffffff80;
      .material-design-icon{
        svg{
          animation: shake 0.5s ease-in 0.1s;
        }
      }
      &::before{
        transform: skew(45deg) translateX(-220%);
      }
    }
  }
  .media-icon+.media-icon{
    margin-left: 10px;
  }
  #my-pic{
    border-radius: 100%
  }
  #my-email{
    font-size: 16px;
    .material-design-icon{
      vertical-align: middle;
    }
  }
  @media (max-width: 425px) {
    width: 35vh;
  }
}

@keyframes shake {
  0% {
    transform: rotate(45deg);
  }
  20% {
    transform: rotate(-40deg);
  }
  40% {
    transform: rotate(30deg);
  }
  60% {
    transform: rotate(-25deg);
  }
  80% {
    transform: rotate(15deg)
  }
  90% {
    transform: rotate(-5deg);
  }
  95% {
    transform: rotate(-2deg);
  }
  100% {
    transform: rotate(0deg);
  }
}
</style>
