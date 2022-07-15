<template>
  <div class="bubble-wrapper">
    <div ref="bubble" class="bubble">
      <img class="bubble-image" :src="currentLogo" />
    </div>
    <div ref="bubblePulse" class="bubble-pulse"></div>
  </div>
</template>

<script>
import { TimelineLite, Back, Elastic, Expo } from "gsap";

export default {
  name: "App",
  components: {},
  methods: {
    randomiseLogo() {
      const logosToSample = this.logos.filter(
        (logo) => logo !== this.currentLogo
      );
      this.currentLogo =
        logosToSample[Math.floor(Math.random() * logosToSample.length)];
    },
  },

  data() {
    return {
      timeline: null,
      logos: [
        "https://www.svgrepo.com/show/33437/boy.svg",
        "https://www.svgrepo.com/show/12676/boy.svg",
        "https://www.svgrepo.com/show/35732/boy.svg",
        "https://www.svgrepo.com/show/45943/boy.svg",
        "https://www.svgrepo.com/show/40673/boy.svg",
        "https://www.svgrepo.com/show/38261/boy.svg",
        "https://www.svgrepo.com/show/45978/boy.svg",
        "https://www.svgrepo.com/show/22032/boy.svg",
        "https://www.svgrepo.com/show/45966/boy.svg",
        "https://www.svgrepo.com/show/34979/boy.svg",
        "https://www.svgrepo.com/show/3852/boy.svg",
        "https://www.svgrepo.com/show/45934/boy.svg",
        "https://www.svgrepo.com/show/10308/boy.svg",
        "https://www.svgrepo.com/show/45814/boy.svg",
         'https://www.svgrepo.com/show/31130/boy.svg',
      ],
      currentLogo: "",
    };
  },

  mounted() {
    const { bubble, bubblePulse } = this.$refs;
    const timeline = new TimelineLite({
      onComplete: () => {
        this.randomiseLogo();
        timeline.restart();
      },
    });

    timeline.to(bubble, 0.4, {
      scale: 0.8,
      rotation: 16,
      ease: Back.easeOut.config(1.7),
    });
    timeline.to(
      bubblePulse,
      0.5,
      {
        scale: 0.9,
        opacity: 1,
      },
      "-=0.6"
    );

    timeline.to(bubble, 1.2, {
      scale: 1,
      rotation: "-=16",
      ease: Elastic.easeOut.config(2.5, 0.5),
    });
    timeline.to(
      bubblePulse,
      1.1,
      {
        scale: 3,
        opacity: 0,
        ease: Expo.easeOut,
      },
      "-=1.2"
    );
  },
};
</script>

<style>
.bubble-wrapper {
  position: relative;
}

.bubble {
  position: relative;
  z-index: 2;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 1px solid white;
  background: #272727;
  border-radius: 50%;
  height: 100px;
  width: 100px;
}

.bubble-pulse {
  position: absolute;
  z-index: 1;
  height: 120px;
  width: 120px;
  top: 50%;
  left: 50%;
  margin-top: -60px;
  margin-left: -60px;
  background: #272727;
  border-radius: 50%;
  opacity: 0;
  transform: scale(0);
}

.bubble-image {
  height: 50%;
}

/* Global Styles */
body {
  background: #1a1a1a;
  padding-top: 80px;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
