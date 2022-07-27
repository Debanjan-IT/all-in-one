<template>
  <div>
    <div class="home-container">
      <h1>All in one downloader</h1>
      <img src="../static/logo.png" alt="Logo" height="30%" width="30%" />
    </div>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  layout: 'main',
}
</script>

<style>
.home-container {
  margin: 0;
  position: absolute;
  top: 50%;
  text-align: center;
  -ms-transform: translateY(-50%);
  transform: translateY(-50%);
}
</style>