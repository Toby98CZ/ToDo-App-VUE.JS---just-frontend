<template>
  <!--<div id="nav">
    <router-link :to="{ name: `Home` }">Home</router-link>|
    <router-link :to="{ name: `About` }">About</router-link>
  </div>
  -->
  <div>
    <span @click="openCloseNav" id="navBtn">&#9776;</span>

    <div id="mySidenav" class="sidenav">
      <!-- <img alt="Vue logo" src="../assets/logo.png" class="logo" />-->
      <a href="javascript:void(0)" class="closebtn" @click="openCloseNav">&times;</a>
      <router-link :to="{ name: `Home` }">Todos</router-link>
      <router-link :to="{ name: `About` }">About app</router-link>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      navigationOpened: false
    };
  },
  methods: {
    openCloseNav() {
      this.navigationOpened = !this.navigationOpened;
      if (this.navigationOpened) {
        document.getElementById("mySidenav").style.width = "250px";
        document.getElementById("app").style.marginLeft = "250px";
      } else {
        document.getElementById("mySidenav").style.width = "0px";
        document.getElementById("app").style.marginLeft = "0px";
      }
    }
  }
};
</script>

<style>
#navBtn {
  font-size: 40px;
  cursor: pointer;
  position: fixed;
  float: left;
  left: 0;
  padding: 25px;
  font-weight: bold;
  color: #cacaca;
}
.sidenav {
  text-align: left;
  height: 100%;
  width: 0;
  position: fixed;
  z-index: 1;
  top: 0;
  left: 0;
  background-color: #111;
  overflow-x: hidden;
  transition: 0.5s;
  padding-top: 60px;
}

.sidenav a {
  padding: 8px 8px 8px 32px;
  text-decoration: none;
  font-size: 25px;
  color: #818181;
  display: block;
  transition: 0.3s;
}

.sidenav a:hover {
  color: #f1f1f1;
}

.sidenav .closebtn {
  position: absolute;
  top: 0;
  right: 25px;
  font-size: 36px;
  margin-left: 50px;
}

#app {
  transition: margin-left 0.5s;
}

@media screen and (max-height: 450px) {
  .sidenav {
    padding-top: 15px;
  }
  .sidenav a {
    font-size: 18px;
  }
}
</style>
