<template>
  <div class="mew-component--banner-ads cursor--pointer">
    <white-sheet class="overflow--hidden">
      <v-carousel
        v-model="currentSlide"
        height="100%"
        hide-delimiters
        show-arrows-on-hover
        cycle
      >
        <v-carousel-item :ripple="false">
          <a :href="browserLink" target="_blank" @click="trackEnkrypt">
            <img
              class="slide-img"
              src="@/assets/images/slides/slide1.jpg"
              alt="Enkrypt"
            />
          </a>
        </v-carousel-item>
        <v-carousel-item :ripple="false">
          <a @click="openMewWallet">
            <img
              class="slide-img"
              src="@/assets/images/slides/slide2.jpg"
              alt="Enkrypt"
            />
          </a>
        </v-carousel-item>
        <v-carousel-item
          :ripple="false"
          :to="{ name: ROUTES_HOME.BUY_HARDWARE_WALLET.NAME }"
          target="_blank"
          @click="trackHardware"
        >
          <img
            class="slide-img"
            src="@/assets/images/slides/slide3.jpg"
            alt="Enkrypt"
          />
        </v-carousel-item>
      </v-carousel>
    </white-sheet>
  </div>
</template>

<script>
import { ROUTES_HOME } from '@/core/configs/configRoutes';
import enkryptMarketing from '@/core/mixins/enkryptMarketing.mixin.js';
import handlerAnalytics from '@/modules/analytics-opt-in/handlers/handlerAnalytics.mixin.js';
export default {
  mixins: [enkryptMarketing, handlerAnalytics],
  data: () => ({
    currentSlide: 0,
    ROUTES_HOME: ROUTES_HOME
  }),
  methods: {
    openMewWallet() {
      if (this.consentToTrack) {
        this.$amplitude.track('WalletSlideMEWWallet', {
          network: this.network.type.name
        });
      }
      // eslint-disable-next-line
      window.open('https://download.mewwallet.com/?source=mew_web', '_blank');
    },
    trackEnkrypt() {
      if (this.consentToTrack) {
        this.$amplitude.track('WalletSlideEnkrypt', {
          network: this.network.type.name
        });
      }
    },
    trackHardware() {
      if (this.consentToTrack) {
        this.$amplitude.track('WalletSlideHardware', {
          network: this.network.type.name
        });
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.slide-img {
  width: 100%;
  height: 100%;
}
</style>
