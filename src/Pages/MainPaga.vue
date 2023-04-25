<template>
  <div class="mainpage">
    <div class="sidebar">
      <router-link class="link" to="/mainPage">supliers</router-link>
      <router-link class="link" to="/clients">clients</router-link>
    </div>
    <div class="mainlist">

      <router-view></router-view>
    </div>
  </div>
</template>

<script setup>

</script>

<style  scoped>
.mainpage {
  display: flex;
  background-color: #fafcf5;
}

h1 {
  color: blue;
  text-align: center;
  margin: 20px 0 60px 0;
}

.sidebar {
  position: sticky;
  top: 0;
  right: 0;
  background-color: #00000014;
  width: 25%;
  height: 100vh;
}

.mainlist {
  margin-left: 3%;
  width: 77%;
  padding-right: 20px;
}

.link {
  text-decoration: none;
  color: blue;
  display: block;
  width: 90%;
  padding: 8px 10px;
  margin: 0 auto;
  background-color: white;
  margin-bottom: 20px;
  border-radius: 10px;
  font-size: 20px;
  font-family: sans-serif;
  font-weight: 600;
  font-family: sans-serif;

}

.link:hover {
  background-color: rgb(219, 163, 163);
}

/* .link:active{
   background-color: black;
   color: red;
 } */ 

 .router-link-active{
    color:red;
 }

</style>