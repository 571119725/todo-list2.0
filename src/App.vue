<template>
    <div class="father">
      <Header />
      <Body />
      <Footer/>
    </div>
</template>

<script>
import Header from './components/Header.vue'
import Body from '/src/Body.vue'
import Footer from './components/Footer.vue'
export default {
  name: 'App',
  components:{
    Header,
    Body,
    Footer
  }
}
</script>

<style>
body {
  background:#f5f5f5;
}
*{
    margin: 0px;
    padding: 0px;
}
img{
    user-select: none;
    cursor: default;
    pointer-events: none;
}
.father{
    display:flex;
    flex-direction:column;
    justify-items: flex-start;
    align-items: center;
    min-width:900px;
    background-color: #f5f5f5;
}
</style>
