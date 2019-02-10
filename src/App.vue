<template>
  <div id="app">
    <DirectionBtn opts="Our Work"/>
  </div>
</template>

<script>
import DirectionBtn from './components/DirectionBtn.vue'

export default {
  name: 'app',
  components: {
    DirectionBtn
  }
}
</script>

<style>
body{
  font-family: 'Ubuntu', serif;
  color: #181829;
  background-size: cover;
  cursor: pointer;
}

.btn{
  border: 3px solid #5BCE8B;
    border-radius: 2px;
    font-family: "Ubuntu";
    font-weight: lighter;
  display: block;
  margin: 100px auto;
  max-width: fit-content;
  position: relative;
  overflow: hidden;
}

.btn a{
  padding: 20px;
  display: block;
  text-decoration: none;
  transition: color 0.5s ease-in;
  z-index: 33;
  position: relative;
/*   color: white; */
}

.btn .before{
  z-index: 1;
  position: absolute;
/*   top: -100%; */
  left:0;
  width: 100%;
  height: 100%;
  background: #5BCE8B;
}





</style>
