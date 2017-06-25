<template>
  <div id="app">
    <!-- Size -->
    <div>
      <label>
        <input v-model.number="width" type="number"> Width
      </label>
    </div>
    <div>
      <label>
        <input v-model.number="height" type="number"> Height
      </label>
    </div>
    <!-- Display -->
    <div>
      <label>
        <input v-model.number="showRatio" type="checkbox"> Show Ratio?
      </label>
    </div>
    <!-- Styling -->
    <div>
      <label>
        <input v-model="backgroundColour"> Background Colour
      </label>
    </div>
    <div>
      <label>
        <input v-model="borderColour"> Border Colour
      </label>
    </div>
    <div>
      <label>
        <input v-model.number="borderWidth" type="number"> Border Width
      </label>
    </div>
    <!-- Typography -->
    <div>
      <label>
        <input v-model="fontFamily"> Font Family
      </label>
    </div>
    <div>
      <label>
        <input v-model="fontColour"> Font Colour
      </label>
    </div>
    <div>
      <label>
        <input v-model.number="fontSize" type="number"> Font Size (px)
      </label>
    </div>
    <!-- Image Placeholder -->
    <div>
      <image-placeholder
        :width="width"
        :height="height"
        :show-ratio="showRatio"
        :background-colour="backgroundColour"
        :border-colour="borderColour"
        :border-width="borderWidth"
        :font-family="fontFamily"
        :font-colour="fontColour"
        :font-size="fontSize"

      ></image-placeholder>
    </div>
  </div>
</template>
<script>
import ImagePlaceholder from './components/ImagePlaceholder'
export default {
  components: {
    ImagePlaceholder
  },
  data () {
    return {
      width: 300,
      height: 200,
      showRatio: false,
      backgroundColour: '#eee',
      borderWidth: 1,
      borderColour: '#ccc',
      fontFamily: 'Helvetica, sans-serif',
      fontColour: '#333',
      fontSize: 14
    }
  }
}
</script>
