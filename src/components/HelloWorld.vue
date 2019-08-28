<template>
  <div class="hello">
    <div class="box">box</div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  methods: {
    handleClick () {
      console.log('click div')
    }
  },
  mounted() {
    $('.box').click(() => {
      console.log('div click')
    })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .box{
    width: 200px;
    height: 200px;
    background-color: red;
  }
</style>
