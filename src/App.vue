<template>
<div id="app">
  <keep-alive>
    <router-view/>
  </keep-alive>
</div>
</template>

<style lang="scss">
@import url('./assets/iconfonts/iconfont.css');
@import './assets/styles/iview-reset';
@import './assets/styles/iview-pro';
body,
html {
    width: 100%;
    height: 100%;
    background: #f1f4f5;
}
#app {
    width: 100%;
    height: 100%;
}
</style>
