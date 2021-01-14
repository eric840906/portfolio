<template>
  <div>
    <header>
      <nav class="nav-bar">
        <ul class="nav-links">
          <li>
            <router-link ref="link" class="nav-link" to="/about">About</router-link>
          </li>
          <li>
            <router-link ref="link" class="nav-link" to="/skills">Skills</router-link>
          </li>
          <li>
            <router-link ref="link" class="nav-link" to="/projects">Projects</router-link>
          </li>
          <li>
            <router-link ref="link" class="nav-link" to="/">Contact</router-link>
          </li>
        </ul>
      </nav>
    </header>
  </div>
</template>

<script>
import { gsap } from 'gsap'
export default {
  mounted () {
    const tl = gsap.timeline()
    tl.from('.nav-links li', { duration: 2, opacity: 0, ease: 'elastic', y: 'random(-100%, 100%)', stagger: 0.33 })
  }
}
</script>

<style lang="scss" scoped>
  .nav-links{
    backdrop-filter: blur(5px);
    height: 5vh;
    display: flex;
    justify-content: space-around;
    align-items: center;
    box-shadow: 0 9px 9px -10px #00000087;
    background-color: #359cf703;
    width: 100%;
    li{
      position: relative;
    }
    .nav-link{
      font-weight: bolder;
      font-size: 1.5rem;
      color: #0000006e;
      @media (max-width: 425px) {
        font-size: 15px;
      }
      &::after{
        content: '';
        width: 0px;
        height: 2px;
        background: #2830ba8f;
        position: absolute;
        border-radius: 46px;
        bottom: -8px;
        left: 50%;
        transform: translateX(-50%);
        transition: 0.3s ease;
      }
      &:hover{
        &::after{
          content: '';
          width: 40px;
        }
      }
    }
    .router-link-exact-active{
      color: #2830ba8f;
      &::after{
        content: '';
        width: 40px;
        height: 2px;
        background: #2830ba8f;
        position: absolute;
        border-radius: 46px;
        bottom: -8px;
        left: 50%;
        transform: translateX(-50%);
        transition: 0.3s ease;
      }
    }
  }
</style>
