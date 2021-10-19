<template>
  <div id="app">
    <!-- <div class="title">
      😩 take me back
    </div> -->

    <video class="video-background" autoplay loop muted playsinline>
      <source src="@/assets/sunset_crop.mp4" type="video/mp4" />
    </video>

    <transition name="fade">
      <TextBorder
        :key="siteData[index].url"
        class="radical"
        :text="sliceURL(siteData[index].url)"
        :size="outerSize"
      />
    </transition>

    <transition name="fade">
      <TextBorder
        :key="siteData[index].date"
        class="radical"
        :text="'visited on ' + siteData[index].date.toLowerCase()"
        :size="innerSize"
      />
    </transition>

    <div class="radical stroke outer-shape">
      <div class="radical stroke inner-shape">
        <iframe
          id="past-url"
          :key="siteData[index].url"
          :src="siteData[index].url"
        ></iframe>
      </div>
    </div>

    <button id="back" @click="backInTime()">back</button>
    <button id="forward" @click="forwardInTime()">forward</button>
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
      index: siteDataJSON.siteData.length - 1,
      prevIndex: 0,
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
      console.log("new outer size: ", this.outerSize);

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
      console.log("prev index: ", this.index);

      this.index = this.index + 1;

      if (this.index >= this.siteData.length) {
        this.index = 0;
      }
      console.log("new index: ", this.index);
    },
    forwardInTime() {
      console.log("prev index: ", this.index);

      this.index = this.index - 1;

      if (this.index < 0) {
        this.index = this.siteData.length - 1;
      }
      console.log("new index: ", this.index);
    },
    sliceURL(url) {
      let urlToDisplay = url;
      if (url.length > 70) {
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

  background: gray;
  /* background: url(https://cdn.pixabay.com/photo/2017/03/17/19/37/sky-2152463_1280.jpg); */
  /* background: url(https://unleash.org/wp-content/uploads/2017/01/sky-1280x720.jpg); */

  /* BEACH WAVES COMING IN AND OUT background: url(https://media1.giphy.com/media/l4hLyOGRJWNSR8QQ8/giphy.gif?cid=ecf05e475u1fsbnioaemivo6097512teide6fcbsff5aj004&rid=giphy.gif&ct=g) */

  /* background: url(https://media3.giphy.com/media/l0ExcZR3msPMnknBu/giphy.gif?cid=ecf05e47extt0bvm4kdho597jrikny1z18uknfmwm6hqhv9t&rid=giphy.gif&ct=g); */

  /* background: url(https://media2.giphy.com/media/3oz8xur099boo4N9aU/giphy.gif?cid=ecf05e47lk8f72afxgh856vrlg5rmpwfhhxnspk7epzqzbi4&rid=giphy.gif&ct=g); */
  background-size: cover;
  background-position: fixed;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  -webkit-user-select: none;
  color: white;
  font-size: 16px;
  line-height: 24px;
  overflow: hidden;
  /* width: 100vw; */
  /* height: 100vh; */
  margin: 0px;
  /* cursor: w-resize; */
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
  width: 183.20610687vh; /* 100 * 16 / 9 */
  min-width: 100%;
  min-height: 54.5833333333vw; /* 100 * 9 / 16 */
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

.stroke {
  border: 5px solid white;
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
  font-family: inherit;
  font-style: italic;
  /* font-size: 3em; */
  position: absolute;
  transform: translate(0, -50%);
}

button#back {
  top: 50%;
  left: 10%;
}

button#forward {
  top: 50%;
  right: 8%;
}

button#back:hover {
  cursor: w-resize;
}

button#forward:hover {
  cursor: e-resize;
}

button:hover {
  color: lavender;
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
  .outer-shape {
    width: 300px;
    height: 300px;
  }

  .inner-shape {
    width: 150px;
    height: 150px;
  }

  button#back {
    left: 1%;
  }

  button#forward {
    right: 1%;
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
    left: 1%;
  }

  button#forward {
    right: 1%;
  }
}
</style>
