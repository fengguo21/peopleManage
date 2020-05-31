<template>
  <button @click="click($event)" class="button" :class="{'large':large,'medium':medium,'mini':mini,'basic':basic}">
    <slot>新建</slot>
  </button>
</template>

<script>
export default {
  name: "mtiButton",
  props: {
    large: {
      type: Boolean,
      default: true
    },
    medium: {
      type: Boolean,
      default: false
    },
    mini: {
      type: Boolean,
      default: false
    },
    basic: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    click(e) {
      this.$emit('click', e)
    }
  }
}
</script>

<style lang="less" scoped>
  .button {
    font-size: 18px;
    height: 40px;
    padding: 0 26px;
    font-weight: 500;
    color: #fff;
    background: #fe7300;
    box-shadow: 0px 0em 0px 0px rgba(39, 41, 43, 0.15) inset;
    cursor: pointer;
    display: inline-block;
    outline: none;
    border: none;
    vertical-align: center;
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol", "Liberation Sans", "PingFang SC", "Microsoft YaHei", "Hiragino Sans GB", "Wenquanyi Micro Hei", "WenQuanYi Zen Hei", "ST Heiti", SimHei, SimSun, "WenQuanYi Zen Hei Sharp", sans-serif;
    margin: 0em 0.25em 0em 0em;
    text-transform: none;
    text-shadow: none;
    font-weight: bold;
    font-style: normal;
    text-align: center;
    border-radius: 2px;

    &.basic {
      background: transparent !important;
      border: 1px solid #fe7300;
      color: #fe7300 !important;
      -webkit-box-shadow: none !important;
      box-shadow: none !important;

      &:hover {
        color: #e28560 !important;
      }

      &:active {
        border-color: #ea6c2d;
        color: #db6435 !important;
        box-shadow: 0px 0px 0px 2px #db6435 inset !important;
      }
    }

    &:hover {
      background: #f38d30;
      -webkit-box-shadow: none;
      box-shadow: none;
    }

    &:active {
      background: #ea6c2d;
    }

    &.medium {
      height: 32px;
      font-size: 1rem;
      font-weight: normal;
      border-radius: 2px;
      padding: 0 10px;
    }

  }
</style>
