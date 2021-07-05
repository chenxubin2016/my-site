<template>
  <div class="signature">
    <div class="signature-content">
      <h3 class="title">电子签名</h3>
      <canvas id="canvas"></canvas>
      <div class="tools">
        <button>清除画板</button>
        <button>下载签名</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ShowCanvas",
  data() {
    return {};
  },
  mounted() {
    this.fileToCanvas();
  },
  methods: {
    fileToCanvas() {
      const canvas = document.getElementById("canvas");
      const ctx = canvas.getContext("2d");
      const img = new Image();
      img.src = require("../assets/long.png");
      // img.src = require("../assets/bj.jpeg");
      img.onload = function () {
        canvas.width = img.width;
        canvas.height = img.height;
        ctx.drawImage(img, 0, 0);
        const imageData = ctx.getImageData(0, 0, img.width, img.height).data;
        console.log(imageData);
        ctx.fillStyle = "#ffffff";
        ctx.fillRect(0, 0, img.width, img.height);
        var gap = 6;
        var dragonContainer = document.getElementById("container");
        var dragonScale = 2;
        for (var h = 0; h < img.height; h += gap) {
          for (var w = 0; w < img.width; w += gap) {
            console.log(w, h);
            var position = (img.width * h + w) * 4;
            var r = imageData[position],
              g = imageData[position + 1],
              b = imageData[position + 2];

            if (r + g + b == 0) {
              ctx.fillStyle = "#000";
              ctx.fillRect(w, h, 4, 4);
            }
            if (r + g + b == 0) {
              var bubble = document.createElement("img");
              bubble.src = require("../assets/bubble.png");
              bubble.setAttribute("class", "bubble");

              var bubbleSize = Math.random() * 10 + 20;
              bubble.style.position = "absolute";
              bubble.style.left = w * dragonScale - bubbleSize / 2 + "px";
              bubble.style.top = h * dragonScale - bubbleSize / 2 + "px";
              bubble.style.width = bubble.style.height = bubbleSize + "px";
              bubble.style.transform = `translate(180px, -20px)`;
              bubble.style.animationDuration = Math.random() * 6 + 4 + "s";

              dragonContainer.appendChild(bubble);
            }
          }
        }
      };
    },
  },
};
</script>

<style lang='scss' scoped>
.signature {
  width: 100%;
  height: calc(100vh - 60px);
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: row;
  .signature-content {
    border: 1px solid #e7e7e7;
    .title {
      height: 44px;
      line-height: 44px;
      margin: 0;
      text-align: center;
      border-bottom: 1px solid #e7e7e7;
    }
    .tools {
      height: 50px;
      padding: 0 20px;
      border-top: 1px solid #e7e7e7;
      display: flex;
      justify-content: flex-start;
      align-items: center;
      flex-direction: row;
      button {
        margin-right: 10px;
        height: 30px;
        // line-height: 30px;
      }
    }
  }
}
</style>
