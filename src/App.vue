<template>
  <div id="app">
    <Navbar></Navbar>
    <div class="wave"></div>
    <div class="bubble circle"></div>
    <div class="bubble circle"></div>
    <div class="bubble circle"></div>
    <div class="bubble circle2"></div>
    <div class="bubble circle3"></div>
    <div class="glass-window">
      <transition name="switch">
        <router-view/>
      </transition>
    </div>
  </div>
</template>

<script>
import { gsap } from 'gsap'
import Navbar from './components/Navbar.vue'
export default {
  components: {
    Navbar
  },
  mounted () {
    document.addEventListener('mousemove', (event) => {
      gsap.to('.wave', {
        x: event.pageX,
        y: event.pageY,
        stagger: -0.1
      })
    })
    gsap.from('.glass-window', { duration: 3, scale: 0.5, ease: 'elastic' })
    const object = {
      el: '.circle',
      duration: 5
    }
    gsap.fromTo(object.el, object.duration, {
      opacity: 1,
      y: 130,
      x: 0,
      scale: 1.5,
      transformOrigin: 'center',
      rotate: 290
    },
    {
      opacity: 0,
      y: '-800',
      x: Math.PI * 2,
      rotate: 180,
      modifiers: {
        x: function (x) {
          return Math.sin(parseFloat(x)) * 200 + 'px'
        }
      },
      scale: 0,
      stagger: {
        each: object.duration / document.querySelectorAll(object.el).length,
        repeat: -1
      }
    })
    const object2 = {
      el: '.circle2',
      duration: 3
    }
    gsap.fromTo(object2.el, object2.duration, {
      opacity: 1,
      y: 130,
      x: 0,
      scale: 1.5,
      transformOrigin: 'center',
      rotate: 290
    },
    {
      opacity: 0,
      y: '-1000',
      x: Math.PI * 2,
      rotate: 180,
      modifiers: {
        x: function (x) {
          return Math.cos(parseFloat(x)) * 200 + 'px'
        }
      },
      scale: 0,
      stagger: {
        each: object.duration / document.querySelectorAll(object.el).length,
        repeat: -1
      }
    })
    const object3 = {
      el: '.circle3',
      duration: 8
    }
    gsap.fromTo(object3.el, object3.duration, {
      opacity: 1,
      y: 130,
      x: 0,
      scale: 1.5,
      transformOrigin: 'center',
      rotate: 0
    },
    {
      opacity: 0,
      y: '-900',
      x: Math.PI * 2,
      rotate: 250,
      modifiers: {
        x: function (x) {
          return Math.cos(parseFloat(x)) * 400 + 'px'
        }
      },
      scale: 0,
      stagger: {
        each: object.duration / document.querySelectorAll(object.el).length,
        repeat: -1
      }
    })
  },
  watch: {
    $route (to, from) {
      document.querySelector('.glass-window').style.overflow = 'hidden'
    }
  },
  updated () {
    setTimeout(() => {
      document.querySelector('.glass-window').style.overflow = 'auto'
    }, 1300)
  }
}
</script>

<style lang="scss">
@import '@/assets/style/scss/main.scss';
#app {
  font-family: 'Quicksand', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background-image: linear-gradient(140deg, white, #0082c673), linear-gradient(180deg, #fbfeff, #4636ff);
  height: 100vh;
  position: relative;
  overflow: hidden;
  color: #0000006e;
  .glass-window{
    margin: auto;
    border: 1px solid #ffffff54;
    background-clip: padding-box;
    box-shadow: 10px 10px 10px #0000002b;
    z-index: 999;
    backdrop-filter: blur(5px);
    border-radius: 10px;
    background-image: linear-gradient(135deg, #ffffff00, #4074dd52);
    height: 85vh;
    width: 90%;
    margin-top: 3vh;
    overflow: auto;
    @media (max-width: 425px) {
      width: 99%
    }
  }
  .bubble{
    background-image: linear-gradient(-96deg, white, #0082c673), linear-gradient(15deg, #fbfeff, #4636ff);
    width: 100px;
    height: 100px;
    bottom: 0%;
    border-radius: 100%;
    position: absolute;
  }
  .circle{
    left: 10%;
  }
  .circle2{
    left: 40%;
  }
  .circle3{
    left: 70%;
    width: 300px;
    height: 300px;
    @media (max-width: 425px) {
      width: 100px;
      height: 100px;
    }
  }
  .wave{
    position: absolute;
    pointer-events: none;
    top: 0;
    left: 0;
    width:40px;
    height:40px;
    border-radius:100%;
    background: rgba(255,255,255,0.3);
    transform: translate(-50%, -50%);
    z-index: 0;
    backdrop-filter: drop-shadow(4px 4px 10px blue);
  }
  // .wave3{
  //   z-index:3;
  //   background-size:auto 90%;
  //   animation:w infinite 0.8s forwards;
  // }
  // .wave2{
  //   z-index:4;
  //   background-size:auto 80%;
  //   animation:w infinite 1s forwards;
  // }
  @keyframes w{
    0%{
      width:1px;
      height:1px;
    }
    100%{
      width:80px;
      height:80px;
    }
  }
  }
  .switch-enter-active, .switch-leave-active {
    transition: all 1s ease;
  }
  .switch-enter, .switch-leave-to{
    opacity: 0;
    transform: translateY(5%);
  }
  .switch-enter-to, .switch-leave{
    opacity: 1;
  }

</style>
