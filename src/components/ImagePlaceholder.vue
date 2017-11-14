<template>
  <svg xmlns="http://www.w3.org/2000/svg" :width="imgWidth" :height="imgHeight">
    <rect :width="rectWidth" :height="rectHeight" :style="imgStyle"/>
    <text x="50%" y="50%" :font-size="fontSize" :font-family="fontFamily" :fill="fontColour" text-anchor="middle" alignment-baseline="middle">
      <slot>{{ displayText }}</slot>
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
    percentWidth: Boolean,
    percentHeight: Boolean,
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
    /**
     * @return {Object}
     */
    imgStyle () {
      return {
        fill: this.backgroundColour,
        outlineColor: this.borderColour,
        outlineStyle: 'solid',
        outlineWidth: this.borderWidth + 'px',
        outlineOffset: (this.borderWidth * -1) + 'px'
      }
    },
    /**
     * @return {String}
     */
    displayText () {
      return this.showRatio === false ? this.size : this.ratio
    },
    /**
     * @return {Number|String}
     */
    imgWidth () {
      return this.percentWidth ? `${this.width}%` : this.width
    },
    /**
     * @return {Number|String}
     */
    imgHeight () {
      return this.percentHeight ? `${this.height}%` : this.height
    },
    /**
     * @return {Number|String}
     */
    rectWidth () {
      return this.percentWidth ? '100%' : this.width
    },
    /**
     * @return {Number|String}
     */
    rectHeight () {
      return this.percentHeight ? '100%' : this.height
    },
    /**
     * Formatted size in pixel
     * @return {String}
     */
    size () {
      return this.width + (this.percentWidth ? '%' : '') + 'x' + this.height + (this.percentHeight ? '%' : '')
    },
    /**
     * Formatted ratio
     * @return {String}
     */
    ratio () {
      const ratio = this.getSimplifiedRatio((this.width / this.height))
      return ratio.x + ':' + ratio.y
    },
    /**
     * @return {String|Number}
     */
    internalWidth () {
      return this.percentWidth ? `${this.width}%` : this.width - (this.borderWidth * 2)
    },
    /**
     * @return {String|Number}
     */
    internalHeight () {
      return this.percentHeight ? `${this.height}%` : this.height - (this.borderWidth * 2)
    }
  },
  methods: {
    /**
     * Simplify a ratio to the lowest whole number
     * @param  {Number} ratio
     * @return {Object}
     */
    getSimplifiedRatio (ratio) {
      const negative = this.isNegative(ratio)
      if (negative) {
        ratio *= -1
      }
      const numerators = [0, 1]
      const denominators = [1, 0]
      const maxNumerator = this.getMaxNumerator(ratio)
      let ratio2 = ratio
      let calcD
      let prevCalcD = NaN
      for (var i = 2; i < 1000; i++) {
        const L2 = Math.floor(ratio2)
        numerators[i] = L2 * numerators[i - 1] + numerators[i - 2]
        if (Math.abs(numerators[i]) > maxNumerator) break
        denominators[i] = L2 * denominators[i - 1] + denominators[i - 2]
        calcD = numerators[i] / denominators[i]
        if (calcD === prevCalcD) break
        if (calcD === ratio) break
        prevCalcD = calcD
        ratio2 = 1 / (ratio2 - L2)
      }

      if (negative) {
        numerators[i] *= -1
      }

      return {
        x: numerators[i],
        y: denominators[i]
      }
    },

    /**
     * Get the fraction numerator of the decimal ratio
     * @param  {Number} ratio - as decimal
     * @return {Number}
     */
    getMaxNumerator (ratio) {
      let ratio2 = this.getScientificRatio(ratio)
      ratio2 = this.getDigits(ratio2)
      let i
      const numDigitsPastDecimal = this.getNumDigitsPastDecimal(ratio, ratio2)

      for (i = numDigitsPastDecimal; i > 0 && ratio2 % 2 === 0; i--) {
        ratio2 /= 2
      }
      for (i = numDigitsPastDecimal; i > 0 && ratio2 % 5 === 0; i--) {
        ratio2 /= 5
      }

      return ratio2
    },

    isNegative (ratio) {
      return ratio < 0
    },

    getScientificRatio (ratio) {
      var scientific = ratio.toString().indexOf('E')
      if (scientific === -1) {
        scientific = ratio.toString().indexOf('e')
      }
      if (scientific === -1) {
        return ratio.toString()
      }
      return ratio.toString().substring(0, scientific)
    },

    getDigits (ratio) {
      let decimal = ratio.toString().indexOf('.')
      if (decimal === -1) {
        return ratio
      }
      if (decimal === 0) {
        return ratio.substring(1, ratio.length)
      }
      if (decimal < ratio.length) {
        return ratio.substring(0, decimal) + ratio.substring(decimal + 1, ratio.length)
      }
      return null
    },

    getNumDigitsPastDecimal (ratio, ratio2) {
      var numDigits = ratio2.toString().length
      var numIntDigits = ratio.toString().length
      if (ratio === 0) {
        numIntDigits = 0
      }
      return numDigits - numIntDigits
    }
  }
}
</script>
