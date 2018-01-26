<template lang="html">
  <nav :class="(this.scrollAmount > 20)?'c-navbar c-navbar--is-scrolled':'c-navbar'" role="navigation" aria-label="main navigation">
    <div class="o-wrapper o-wrapper--in-fixed-navbar">
      <div :class="isActive ? 'c-navbar__brand c-navbar__brand--active' : 'c-navbar__brand' ">
        <button @click="isActive = !isActive">
          <span></span>
          <span></span>
          <span></span>
        </button>
      </div>
      <div :class="isActive ? 'c-navbar__menu c-navbar__menu--active':'c-navbar__menu'">
        <router-link class="c-navbar__link" to="/" active-class="c-navbar__link--active" :exact="true">
          <span>Home</span>
        </router-link>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  data () {
    return {
      isActive: false,
      scrollAmount: 0
    }
  },
  mounted () {
    this.scrollAmount = window.pageYOffset
    this.$el.querySelectorAll('a').forEach((node) => {
      node.addEventListener('click', this.onLinkClick)
    })
    document.addEventListener('scroll', this.onScroll)
  },
  methods: {
    onScroll () {
      this.scrollAmount = window.pageYOffset
    },
    onLinkClick () {
      if (this.isActive) this.isActive = !this.isActive
    }
  }
}
</script>

<style lang="scss">
  .c-navbar {
    @include mq($from: mobile, $until: desktop) {
      background-color: $color-background;
    }
    @include mq($from: desktop) {
      display: flex;
      // max-width: $inuit-wrapper-width;
      // margin: 0 auto;
      // padding: 3rem $inuit-global-spacing-unit 0;
      padding-top: 3rem;
      position: fixed;
      width: 100%;
      top: 0;
      left: 0;
      z-index: 999;
      transition: padding-top .2s linear;
    }
  }
  .c-navbar--is-scrolled {
    @include mq($from: desktop) {
      transition: padding-top .2s linear;
      padding-top: 0;
      background-color: $color-background;
      border-bottom: solid 1px $color-link;
    }
  }
  .c-navbar__brand {
    button {
      @include mq($from: mobile, $until: desktop) {
        align-self: stretch;
        cursor: pointer;
        display: block;
        height: 3.25rem;
        position: relative;
        width: 3.25rem;
        margin-left: auto;
        background-color: transparent;
        border: none;
        outline: none;
        transition: all .3s ease-in-out;
        span {
          display: block;
          height: 1px;
          left: calc(50% - 8px);
          position: absolute;
          background-color: $color-text;
          width: 16px;
          transition: all .2s ease-in-out;
          transform-origin: center;
          &:nth-child(1) {
            transform: translate(0, -5px);
          }
          &:nth-child(2) {
            opacity: 1;
          }
          &:nth-child(3) {
            transform: translate(0, 5px);
          }
        }
      }
      @include mq($from: desktop) {
        display: none;
      }
    }
    &.c-navbar__brand--active {
      button {
        @include mq($from: mobile, $until: desktop) {
          background-color: lighten($color-background, 10);
          span {
            transition: all .2s ease-in-out;
            &:nth-child(1) {
              transform: translate(0, 0) rotate(45deg);
            }
            &:nth-child(2) {
              opacity: 0;
            }
            &:nth-child(3) {
              transform: translate(0, 0)  rotate(-45deg);
            }
          }
        }
      }
    }
  }
  .c-navbar__menu {
    @include mq($from: mobile, $until: desktop) {
      height: 0;
      margin-left: -1rem;
      margin-right: -1rem;
      transition: height .3s ease-in-out, opacity .1s ease-in-out;
      opacity: 0;
      display: flex;
      flex-direction: column;
      &.c-navbar__menu--active {
        height: 2.25 * 4rem;
        opacity: 1;
      }
    }
  }
  .c-navbar__link {
    padding: 0 1rem;
    text-transform: uppercase;
    @include mq($from: mobile, $until: desktop) {
      line-height: 2.25rem;
    }
    @include mq($from: desktop) {
      line-height: 3.25rem;
      &:nth-child(1) {
        padding-left: 0
      }
    }
  }
  .c-navbar__link--active {
    span {
      font-weight: 700;
      border-bottom: solid 2px $color-link;
    }
  }
</style>
