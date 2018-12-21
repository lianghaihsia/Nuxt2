<template>
  <div>
    <div class="diss">
      <!-- <img src="~static/timg.jpg" alt=""> -->
    </div>
    <ul>
      <li><nuxt-link :to="{name:'index'}">HOME</nuxt-link></li>
      <li><nuxt-link :to="{name:'about'}">ABOUT</nuxt-link></li>
      <li><nuxt-link :to="{name:'news',params:{newsId: 3301}}">NEWS</nuxt-link></li>
      <li><nuxt-link :to="{name:'asyncData'}">asyncData</nuxt-link></li>
    </ul>
  </div>
</template>

<script>
import AppLogo from '~/components/AppLogo.vue'

export default {
  components: {
    AppLogo
  }
}
</script>

<style>
.diss{
  width: 300px;
  height: 100px;
  background-image: url(~static/timg.jpg)
}
</style>

