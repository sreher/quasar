<template>
  <div class="q-layout-padding docs-touch row justify-center">
    <div style="width: 500px; max-width: 90vw;">
      <p class="caption">
        <span class="desktop-only">Click and hold with your mouse</span>
        <span class="mobile-only">Touch and hold</span>
        on the area below to see it in action.
        <br>
        Notice that on touch capable devices the scrolling is not blocked.
      </p>

      <div
        v-touch-hold.mouse="handleHold"
        @click="onClick"
        class="custom-area row flex-center"
      >
        <div v-if="info" class="custom-info">
          <pre>{{ info }}</pre>
        </div>
        <div v-else class="text-center q-pa-xl custom-area-placeholder">
          Click/touch and hold for at least 600ms.
        </div>
      </div>

      <p class="caption">
        Configuring to trigger after custom time (in this case 3s):
      </p>
      <div
        v-touch-hold:3000.mouse="holdExtended"
        @click="onClick"
        class="custom-area row flex-center"
      >
        <div v-if="infoExtended" class="custom-info">
          <pre>{{ infoExtended }}</pre>
        </div>
        <div v-else class="q-pa-xl custom-area-placeholder">
          Click/touch and hold for 3 seconds
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import './touch-style.styl'

export default {
  data () {
    return {
      info: null,
      infoExtended: null
    }
  },
  methods: {
    handleHold ({ position, duration, evt }) {
      this.info = { position, duration }

      // native Javascript event
      console.log(evt)
    },
    holdExtended ({ position, duration, evt }) {
      this.infoExtended = { position, duration }

      // native Javascript event
      console.log(evt)
    },

    onClick (ev) {
      console.log('click', ev.type, ev)
    }
  }
}
</script>
