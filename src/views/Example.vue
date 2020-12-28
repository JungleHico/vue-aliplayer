<template>
  <div>
    <ali-player
      ref="player"
      source="//player.alicdn.com/video/editor.mp4"
      width="100%"
      height="500px"
      :preload="true"
      :useH5Prism="true"
      @pause="onPause">
    </ali-player>
  </div>
</template>

<script>
import Aliplayer from "../components/Aliplayer"

export default {
  components: {
    "ali-player": Aliplayer
  },
  data() {
    return {
      
    }
  },
  methods: {
    onPause() {
      console.log('pause')
      if (this.$refs.player) {
        console.log(this.$refs.player.getCurrentTime())
      }
    }
  },
}
</script>

<style scoped>

</style>
