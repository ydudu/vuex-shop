<template>
  <header class="app-header">
    <h3 class="app-header-title">{{title}}</h3>
  </header>
</template>

<script>
    export default {
        name: "Header",
        props:["title"]
    }
</script>

<style lang="stylus">

  .app-header
    text-align: center
    height: 45px
    line-height: 45px
</style>
