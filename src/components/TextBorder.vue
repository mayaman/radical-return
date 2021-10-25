<template>
  <div
    class="border"
    v-bind:style="{ width: size + 'px', height: size + 'px' }"
  >
    <fieldset>
      <legend>{{ text }}</legend>
    </fieldset>
    <fieldset>
      <legend>{{ text }}</legend>
    </fieldset>
    <fieldset>
      <legend>{{ text }}</legend>
    </fieldset>
    <fieldset>
      <legend class="four">{{ text }}</legend>
    </fieldset>
  </div>
</template>

<script>
export default {
  name: "TextBorder",
  props: {
    text: String,
    size: Number,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
div.border {
  display: grid;
  margin: auto;
  /* font-family: cursive; */
  /* font-style: italic; */
}

fieldset {
  border: 1px solid transparent;
  border-top-color: #000000;
  box-sizing: border-box;
  grid-area: 1 / 1;
  border: none;
  width: inherit;
}


fieldset:nth-of-type(1) {
  background: content-box center/contain no-repeat;
}

fieldset:nth-of-type(2) {
  transform: rotate(90deg);
}

fieldset:nth-of-type(3) {
  transform: rotate(180deg);
}

fieldset:nth-of-type(4) {
  transform: rotate(-90deg);
}

legend {
  /* font: 15pt/0 'Averia Serif Libre'; */
  margin: auto;
  padding: 3px 0px;
  /* background: hotpink; */
}

legend.four {
  padding: 0px 0px;
}


fieldset:nth-of-type(3) > legend {
  transform: rotate(180deg);
}

</style>
