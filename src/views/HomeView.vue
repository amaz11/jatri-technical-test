<script setup>
import Table from '../components/Table.vue'
</script>

<template>
  <div class="img">
    <img src="https://www.jatri.co/_nuxt/jatri-logo.19582a96.svg" alt="jatri">
    <h1>Technical Test</h1>
</div>
<div>
  <h3>Participant</h3>
  <div class="profile">
    <div class="profile-img">
      <img src="https://avatars.githubusercontent.com/u/73777861?v=4" alt="">
    </div>
    <h4>K M Amaz Uddin Shaon</h4>
  </div>
  <div class="fileLink">
    <a href="https://github.com/amaz11/jatri-technical-test">Github Code File</a>
    <a href="https://admirable-bunny-b24fa0.netlify.app/">Live Demo</a>
  </div>
</div>
<div class="table">
  <Table />
</div>
</template>

<style scoped>
.img{
  text-align: center;
  padding: 8px 0px;
}

h1{
  font-size: 32px;
  font-weight: 800;
  color: rgb(66, 66, 66);

}
h3{
  font-size: 24px;
  font-weight: 600;
  color: rgb(66, 66, 66);
}
.profile{
  display: flex;
  align-items: center;
  gap: 5px;
  margin: 5px 0;
}
.fileLink{
  display: flex;
  flex-direction: column;
  margin-top: 5px;
}

.fileLink a{
  font-weight: 500;
  color: #00A372;
  text-decoration: none;
}
.profile h4{
  font-size: 20px;
  font-weight: 500;
  color: rgb(66, 66, 66);
}
.profile-img{
  width: 50px;
  height: 50px;
  border-radius: 50%;
}
.profile-img img{
  width: 100%;
  border-radius: 50%;
}
.table {
  margin: 12px 0;
}
</style>
