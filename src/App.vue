<template>
  <div id="app">
    <div id="nav">
      PHDiscover.com (COMING SOON)
    </div>
    <router-view/>
  </div>
</template>

<style>
  *,
  *::after,
  *::before {
    box-sizing: inherit;
  }
  html {
    box-sizing: border-box;
  }
  body {
    padding: 0;
    margin: 0;
  }
  #nav {
    background: #333;
    color: #FFF;
    font-family: Arial, Helvetica, sans-serif;
    font-size: 18px;
    text-align: center;
    padding: 20px;
  }
  h1,h2,h3,h4,h5 {
    margin: 0;
  }
</style>
