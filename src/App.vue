<template>
  <div id="app">
    <v-select class="select"></v-select>
    <v-list class="list"></v-list>
    <v-content class="content"></v-content>
  </div>
</template>

<script type="ecmascript-6">
  import Select from './components/select.vue'
  import List from './components/list.vue'
  import Content from './components/content.vue'

  export default {
    name: 'app',
    components: {
      'v-select': Select ,
      'v-list': List,
      'v-content': Content
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  #app
    font-family 'Helvetica Neue',Helvetica,Arial,sans-serif
    -webkit-font-smoothing antialiased
    -moz-osx-font-smoothing grayscale
    text-align center
    display flex
    height 100%
    .select
      flex 0 0 80px
      width 80px
      height 100%
      overflow hidden
    .list
      flex 0 0 300px
      width 300px
      height 100%
      overflow hidden
    .content
      flex 1
      height 100%
      overflow hidden
</style>
