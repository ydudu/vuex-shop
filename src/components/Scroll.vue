<template>
  <section id="goods" class="goods-box" ref="scroll">
    <slot></slot>
  </section>
</template>

<script>
    import BScroll from 'better-scroll'
    export default {
        name: "Scroll",
        mounted(){
          this.$nextTick(() => {
            let scrollBox = this.$refs.scroll;
            this.scroll = new BScroll(scrollBox, {
              click: true
            })
        })
        }
    }
</script>

<style lang="stylus">
  .goods-box
    padding: 0 20px
    position: relative;
    width: 100%;
    height: 100%;
    overflow: hidden;
</style>
