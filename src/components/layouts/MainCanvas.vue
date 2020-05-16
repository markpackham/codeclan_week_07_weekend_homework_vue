<template>
  <div>
    <canvas id="canvas" width="490" height="50"></canvas>
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
    const text = "All data taken from Studio Ghibli API";
    ctx.fillStyle = "#f0e2e1";
    ctx.fillRect(0, 0, canvas.width, canvas.height);
    ctx.font = "30px Palatino sans-serif";
    ctx.textBaseline = "top";
    ctx.shadowColor = "red";
    ctx.shadowOffsetX = 2;
    ctx.shadowOffsetY = 0;
    ctx.shadowBlur = blur;
    ctx.fillStyle = "black";
    ctx.stokeStyle = "black";
    ctx.fillText(text, 10, 10);

    const ctxShape = canvas.getContext("2d");
    ctxShape.beginPath();
    ctxShape.moveTo(1600, 150);
    ctxShape.lineTo(1600, 75);
    ctxShape.lineTo(5, 33);
    ctxShape.fill();
  }
};
</script>

<style>
</style>