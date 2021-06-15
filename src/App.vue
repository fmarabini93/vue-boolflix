<template>
  <div id="app">
    <Main />
  </div>
</template>

<script>
// import axios from 'axios';
import Main from './components/Main';

export default {
  name: 'App',
  components: {
    Main
  }
}
</script>

<style lang="scss">
@import '~@fortawesome/fontawesome-free/css/all.min.css';
@import '~bootstrap/scss/bootstrap.scss';
$red: #dc1a28;

  body {
    background-color: $dark;
  }
</style>
