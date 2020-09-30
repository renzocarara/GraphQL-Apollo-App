<template>
  <div id="app">
     <HeaderComp />
     <transition name="fade" mode="out-in" appear>
        <router-view />
     </transition>
     <FooterComp />
  </div>
</template>


<script>
import HeaderComp from "@/components/HeaderComp.vue";
import FooterComp from "@/components/FooterComp.vue";

export default {
    name: "App",
    components: {
        HeaderComp,
        FooterComp,
    },
};
</script>


<style>
body {
    background-color: #f0f0f0;
}
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
}

.container {
    margin-top: 230px;
    padding: 20px 0;
    background-color: #f0f0f0;
}
/* // --------------------------- TRANSITIONs ----------------------------------- */
/* // transizione in ingresso, per apparire gradualmente */
.fade-enter-active {
    transition: opacity 1.5s;
}
.fade-enter {
    opacity: 0;
}

/* // transizione in uscita, per scomparire gradualmente */
.fade-leave-active {
    transition: opacity 0.5s;
}
.fade-leave-to {
    opacity: 0;
}
</style>
