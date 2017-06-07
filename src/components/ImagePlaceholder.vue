<template>
  <svg xmlns="http://www.w3.org/2000/svg" :width="width" :height="height">
    <rect :x="borderWidth" :y="borderWidth" :width="internalWidth" :height="internalHeight" :style="imgStyle"/>
    <text x="50%" y="50%" font-size="18" text-anchor="middle" alignment-baseline="middle">
      {{ displayText }}
    </text>
  </svg>
</template>

<script>
export default {
  props: {
    width: {
      type: Number,
      default: 200
    },
    height: {
      type: Number,
      default: 150
    },
    backgroundColour: {
      type: String,
      default: '#ccc'
    },
    borderColour: {
      type: String,
      default: '#333'
    },
    borderWidth: {
      type: Number,
      default: 1
    },
    showRatio: {
      type: Boolean,
      default: false
    },
    fontFamily: {
      type: String,
      default: 'monospace, sans-serif'
    },
    fontColour: {
      type: String,
      default: '#333'
    },
    fontSize: {
      type: Number,
      default: 14
    }
  },
  computed: {
    imgStyle () {
      return {
        fill: this.backgroundColour,
        stroke: this.borderColour,
        strokeWidth: this.borderWidth
      }
    },
    displayText () {
      return this.showRatio === false ? this.size : this.ratio
    },
    size () {
      return this.width + 'x' + this.height
    },
    ratio () {
      return this.width > this.height
        ? (this.width / this.height) * 100 / 100 + ':' + this.height / this.height
        : this.width / this.width + ':' + (this.height / this.width) * 100 / 100
    },
    internalWidth () {
      return this.width - (this.borderWidth * 2)
    },
    internalHeight () {
      return this.height - (this.borderWidth * 2)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
