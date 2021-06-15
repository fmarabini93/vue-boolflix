<template>
  <div id="app">
    <Header />
    <Main />
  </div>
</template>

<script>
// import axios from 'axios';
import Header from './components/Header'
import Main from './components/Main';

export default {
  name: 'App',
  components: {
    Header,
    Main
  }
}
</script>

<style lang="scss">
@import '~@fortawesome/fontawesome-free/css/all.min.css';
@import '~bootstrap/scss/bootstrap.scss'
</style>
