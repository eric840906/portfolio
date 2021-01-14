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
    tl.from('.social-media svg', { duration: 1, y: 'random(-100%, 100%)', opacity: 0, stagger: 0.33 })
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
  color: #2830ba8f;
  font-weight: 700;

  *+*{
    margin-top: 10px;
  }
  a{
    color:#2830ba8f;
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
</style>
