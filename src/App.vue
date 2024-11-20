<script>
import AppFooter from "@/components/includes/AppFooter.vue";
import AppHeader from "@/components/includes/AppHeader.vue";
// import 'vue3-toastify/dist/index.css';
export default {
  components: {
    AppHeader,
    AppFooter,
  },
} 
</script>
<template>
  <div id="app m-auto">
    <AppHeader />
    <div class="mt-3">
      <router-view />
    </div>
  </div>
  <AppFooter />
</template>
<style lang="css">
@import "../node_modules/bootstrap/dist/css/bootstrap.min.css";


#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 15px;
}

#nav > a {
  font-weight: bold;
  color: #2c3e50;
  /* &.router-link-exact-active {
    color: #42b983;
  } */
}

html {
  position: relative;
  min-height: 100%;
}
body {
  margin-bottom: 60px; /* Margin bottom by footer height */
}
.footer {
  position: relative;
  bottom: 0;
  width: 100%;
  height: 60px; /* Set the fixed height of the footer here */
  background-color: #f5f5f5;
}

footer {
  background-color: #f2f2f2;
  padding: 25px;
}

.footer p,
.footer div {
  display: inline;
  vertical-align: top;
  font-family: "Open Sans", sans-serif;
  font-size: 16px;
  line-height: 28px;
}
.footer p {
  font-weight: bold;
}

* a {
  color: #42b983;
}

* .fa {
  font-size: 18px;
}

.buttonGreen-outline {
  width: 100%;
  color: #41b883;
  background-color: transparent;
  border-color: #41b883;
}
.buttonGreen-outline:hover {
  color: #ffffff;
  background-color: #41b883;
  border-color: #41b883;
}

.buttonGreen {
  color: #fff;
  background-color: #41b883;
}

.buttonGreen:hover {
  background-color: #42a97b;
}
</style>