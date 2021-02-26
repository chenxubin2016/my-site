<template>
  <div class="flur">
    <h2>Focus</h2>
    <img src="../assets/bj.jpeg" alt="">
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: { msg: String },
  data() {
    return {};
  },
  methods: {}
};
</script>
<style lang="scss" scoped>
  .flur {
    position: relative;
    width: 100vw;
    height: 100vh;
    overflow: hidden;
    display: flex;
    justify-content: center;
    align-items: center;
    h2 {
      position: absolute;
      color: #fff;
      font-size: 5em;
      text-transform: uppercase;
      font-weight: 700;
      z-index: 2;
      transition: 2s;
      &:hover{
        filter: blur(5px);
        transition: 2s;
        transform: scale(1.2);
        & ~ img{
          top: 0;
          left: 0;
          width: 100vw;
          height: 100vh;
          filter: blur(0);
        }
      }
    }
    img{
      position: absolute;
      top:-20%;
      left:-20%;
      width: 140vw;
      height: 140vh;
      pointer-events: none;
      object-fit: cover;
      filter: blur(10px);
      transition: 2s;
    }
  }
</style>
