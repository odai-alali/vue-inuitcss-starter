<template>
  <div class="c-app" id="app">
    <nav-bar></nav-bar>
    <div class="o-wrapper">
      <div class="o-layout o-layout--strech">
        <div class="o-layout__item  u-1/1">
          <home-page></home-page>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import NavBar from '@/components/NavBar'
import HomePage from '@/pages/HomePage'

export default {
  name: 'app',
  components: {
    NavBar,
    HomePage
  }
}
</script>

<style lang="scss">
.c-app {

}
</style>
