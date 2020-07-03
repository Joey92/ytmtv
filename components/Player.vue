<template>
  <div id="player">
    <youtube
      :video-id="videoId"
      :list="playlist"
      ref="youtube"
      @playing="playing"
      @ready="playVideo"
      @cue="cued"
      @error="error"
      fitParent
      :player-vars="playerVars"
    />
    <transition name="overlay">
      <div v-if="showOverlay" id="overlay">
        <h1>Title</h1>
        <h2>Artist</h2>
        <p>Album</p>
      </div>
    </transition>
  </div>
</template>

<script>
const showOverlayPct = () => [5, 90]

export default {
  data () {
    return {
      duration: 1,
      progress: 0,
      overlayPctProgress: showOverlayPct(),
      showOverlay: false,
      playerVars: {
        autoplay: 1,
        modestbranding: 1,
        showinfo: 0,
        origin: 'localhost',
        rel: 0,
        controls: 1 // disable at some point?
      }
    }
  },
  methods: {
    playVideo () {
      this.player.playVideo()
    },
    async playing () {
      this.overlayPctProgress = showOverlayPct() // reset overlay times
      const duration = await this.player.getDuration()
      this.duration = duration
    },
    cued (cue) {
      console.log(cue)
    },
    error (error) {
      console.log(error)
    },
    async update () {
      const time = await this.player.getCurrentTime()
      this.progress = Math.round(time / this.duration * 100)
      if (this.overlayPctProgress.includes(this.progress)) {
        this.overlayPctProgress.shift()
        this.showOverlay = true
        setTimeout(() => {
          this.showOverlay = false
        }, 15000)
      }
    }
  },
  computed: {
    player () {
      return this.$refs.youtube.player
    },
    videoId () {
      return this.$route.query.v.toString()
    },
    playlist () {
      return this.$route.query.list ? this.$route.query.list.toString() : null
    }
  },
  created() {
    setInterval(() => this.update(), 1000) // tricky for videos under 100 sec long, might miss the % trigger for showing the overlay
  }
}
</script>

<style>
#player {
  width: 100%;
  height: 100%;
}

#overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  color: antiquewhite;
  background: rgb(2,0,36);
  background: linear-gradient(90deg, rgba(2,0,36,1) 20%, rgba(0,212,255,0) 100%);
  padding: 10px;
}

.overlay-enter-active, .overlay-leave-active {
  transition: opacity .5s;
}
.overlay-enter, .overlay-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>
