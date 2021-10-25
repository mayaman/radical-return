<template>
  <div id="app">
    <video class="video-background" autoplay loop muted playsinline>
      <source src="@/assets/beach.mp4" type="video/mp4" />
    </video>

    <!-- <video class="video-background" autoplay loop muted playsinline>
      <source src="@/assets/sunset_crop.mp4" type="video/mp4" />
    </video> -->

    <!-- <video class="video-background" autoplay loop muted playsinline>
      <source src="https://cdn.videvo.net/videvo_files/video/free/2015-04/large_watermarked/Ocean_Waves_slow_motion_videvo_preview.mp4" type="video/mp4" />
    </video> -->

    <TextBorder
      :key="siteData[index].url"
      class="radical"
      :text="sliceURL(siteData[index].url)"
      :size="outerSize"
    />

    <TextBorder
      :key="siteData[index].date"
      class="radical"
      :text="'visited on ' + siteData[index].date.toLowerCase()"
      :size="innerSize"
    />

    <div class="radical stroke outer-shape">
      <div class="radical stroke inner-shape">
        <iframe
          id="past-url"
          :key="siteData[index].url"
          :src="siteData[index].url"
        ></iframe>
      </div>
    </div>

    <button id="back" @click="backInTime()">(♥‿♥ ✿)</button>
    <button id="forward" @click="forwardInTime()">(✿ ♥‿♥)</button>
  </div>
</template>

<script>
import TextBorder from "./components/TextBorder.vue";
import siteDataJSON from "./assets/data.json";

export default {
  name: "App",
  components: {
    TextBorder,
  },
  data: function () {
    return {
      index: Math.floor(Math.random() * siteDataJSON.siteData.length - 1),
      siteData: siteDataJSON.siteData,
      outerSize: 680,
      innerSize: 430,
      largeOuterSize: 680,
      largeInnerSize: 430,
      mediumOuterSize: 530,
      mediumInnerSize: 330,
      smallOuterSize: 370,
      smallInnerSize: 220,
      mediumWidthMax: 800,
    };
  },
  created() {
    window.addEventListener("resize", this.handleWindowResize);
  },
  mounted() {
    // console.log(this.siteData);
    // setInterval(() => {
    //   this.updateSite();
    // }, 10000);
    this.handleWindowResize();
  },
  computed: {},
  methods: {
    handleWindowResize() {
      if (window.innerWidth >= 900) {
        this.outerSize = this.largeOuterSize;
        this.innerSize = this.largeInnerSize;
      } else if (window.innerWidth > 600 && window.innerWidth < 900) {
        this.outerSize = this.mediumOuterSize;
        this.innerSize = this.mediumInnerSize;
      } else if (window.innerWidth < 600) {
        this.outerSize = this.smallOuterSize;
        this.innerSize = this.smallInnerSize;
      }
    },
    backInTime() {
      this.index = this.index + 1;

      if (this.index >= this.siteData.length) {
        this.index = 0;
      }
    },
    forwardInTime() {
      this.index = this.index - 1;

      if (this.index < 0) {
        this.index = this.siteData.length - 1;
      }
    },
    sliceURL(url) {
      let urlToDisplay = url;

      let maxURLLength = 70;

      if (window.innerWidth < 600) {
        maxURLLength = 50;
      }

      if (url.length > maxURLLength) {
        urlToDisplay = urlToDisplay.slice(0, 70) + "...";
      }
      return urlToDisplay;
    },
  },
};
</script>

<style>
body {
  min-width: 100vw;
  min-height: 100vh;

  background: lightskyblue;
  background-size: cover;
  background-position: fixed;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  -webkit-user-select: none;
  color: white;
  font-size: 16px;
  line-height: 24px;
  text-shadow: 2px 2px 4px gray;
  overflow: hidden;
  margin: 0px;

  /* font-family: cursive; */
}

#app {
  position: fixed;
  width: 100vw;
  min-width: 100vw;
  height: 100vh;
  min-height: 100vh;
  overflow: hidden;
}

video.video-background {
  height: 100%;
  width: 177.777777778vh; /* 100 * 16 / 9 */
  min-width: 100%;
  min-height: 56.25vw; /* 100 * 9 / 16 */
}

.title {
  position: absolute;
  top: 20px;
  left: 15px;
  /* transform: translate(-50%, -50%); */
  font-size: 2em;
  width: 100%;
  text-align: left;

  font-family: cursive;
  /* display: none; */
}

.radical {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 99999999;
}

iframe {
  /* -webkit-transform: scale(0.2);
    transform: scale(0.2); */
  /* width: 100%;
    height: 100%; */
  border: none;
  width: 200% !important;
  height: 200% !important;
  -webkit-transform: scale(0.5);
  transform: scale(0.5);
  -webkit-transform-origin: 0 0;
  transform-origin: 0 0;
}

.stroke:hover {
  /* box-shadow: 0px 0px 15px white; */
}

.stroke {
  border: 5px solid white;
  box-shadow: 0px 0px 5px lightgray;
}

.outer-shape {
  width: 600px;
  height: 600px;
}

.inner-shape {
  width: 350px;
  height: 350px;
  overflow: hidden;
  background: white;
}

button {
  margin: 5px;
  color: white;
  background: none;
  border: none;

  color: white;
  font-size: inherit;
  line-height: 24px;
  text-shadow: 2px 2px 4px gray;

  font-family: inherit;
  /* font-style: italic; */
  text-align: center;
  position: absolute;
}

button#back {
  top: 50%;
  left: 9%;
  transform: translate(-50%, -50%);
}

button#forward {
  top: 50%;
  right: 9%;
  transform: translate(50%, -50%);
}

button#back:hover {
  cursor: help;
}

button#forward:hover {
  cursor: help;
}

button:hover {
  text-shadow: 2px 2px 10px white;
}

/* .fade-enter-active,
.fade-leave-active {
  transition: opacity 1s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
} */

@media only screen and (max-width: 600px) {
  body {
    font-size: 12px;
    line-height: 18px;
  }

  .outer-shape {
    width: 300px;
    height: 300px;
  }

  .inner-shape {
    width: 150px;
    height: 150px;
  }

  button#back {
    top: 20%;
    left: 50%;
  }

  button#forward {
    left: 50%;
    top: 80%;
    transform: translate(-50%, -50%);
  }
}

@media only screen and (max-width: 900px) and (min-width: 600px) {
  .outer-shape {
    width: 450px;
    height: 450px;
  }

  .inner-shape {
    width: 250px;
    height: 250px;
  }

  button#back {
    left: 5%;
  }

  button#forward {
    right: 5%;
  }
}
</style>
