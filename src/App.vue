<template>
  <div id="app">
    <Calculator/>
    <div class="footer">
      Created By&nbsp;
      <a target="_blank" href="https://twitter.com/RafalWilinski">
        @RafalWilinski
      </a>
    </div>
  </div>
</template>

<script>
import Calculator from './components/Calculator';

export default {
  name: 'app',
  components: {
    Calculator,
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.footer {
  position: absolute;
  bottom: 10px;
  display: flex;
  justify-content: center;
  width: 100%;
}
</style>
