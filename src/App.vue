<template>
  <div id="app">
    <transition name="fade">
      <TextBorder
        :key="siteData[index].url"
        class="radical"
        :text="siteData[index].url"
        size="680"
      />
    </transition>

    <transition name="fade">
      <TextBorder
        :key="siteData[index].date"
        class="radical"
        :text="'Visited on ' + siteData[index].date"
        size="430"
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

    <button @click="updateSite()">回</button>
    <!-- <button v-for="(data, index) in siteData" @click="updateSite(index)">
      {{ siteData[index].date }}
    </button> -->
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
      index: 0,
      prevIndex: 1,
      siteData: siteDataJSON.siteData,
    };
  },
  mounted() {
    // console.log(this.siteData);
    // setInterval(() => {
    //   this.updateSite();
    // }, 10000);
  },
  methods: {
    updateSite() {
      this.index = (this.index + 1) % this.siteData.length;
      if (this.index == 0) {
        this.prevIndex = this.siteData.length - 1;
      } else {
        this.prevIndex = this.index - 1;
      }

      // If there are individual buttons
      // this.index = index;
    },
  },
};
</script>

<style>
body {
  background: gray;
  /* background: url('https://cdn.pixabay.com/photo/2017/03/17/19/37/sky-2152463_1280.jpg'); */
  background: url("https://unleash.org/wp-content/uploads/2017/01/sky-1280x720.jpg")
    no-repeat center center fixed;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;
  background-position: fixed;
  user-select: none;
  -webkit-user-select: none;
  color: white;
  font-size: 18px;
  line-height: 24px;
  overflow: hidden;
}

#app {
  width: 100vw;
  height: 100vh;
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

button:hover {
  cursor: w-resize;
}

/* .fade-enter-active,
.fade-leave-active {
  transition: opacity 3s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
} */
</style>
