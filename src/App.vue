<template>
  <div id="app">
    <image-placeholder :width="200" :height="150" :show-ratio="true"></image-placeholder>
  </div>
</template>
<script>
import ImagePlaceholder from './components/ImagePlaceholder'
export default {
  components: {
    ImagePlaceholder
  }
}
</script>
