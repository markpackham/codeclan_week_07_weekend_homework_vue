<template>
  <div>
    <canvas id="canvas" width="600" height="200"></canvas>
  </div>
</template>

<script>
export default {
  name: "main-canvas",
  data() {
    return {};
  },
  methods: {},
  mounted() {
    const canvas = document.getElementById("canvas");
    const ctx = canvas.getContext("2d");
    const text = "All data taken from, Studio Ghibli API";
    ctx.font = "30px Palatino sans-serif";
    ctx.textBaseline = "top";
    ctx.shadowColor = "red";
    ctx.shadowOffsetX = 2;
    ctx.shadowOffsetY = 0;
    ctx.shadowBlur = blur;
    ctx.fillStyle = "black";
    ctx.fillText(text, 100, 100);
  }
};
</script>

<style>
</style>