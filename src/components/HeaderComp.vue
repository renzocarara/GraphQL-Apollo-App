<template>
  <div class="container-fluid my-header">
    <h2>Star Trek TOS Characters</h2>
    <img alt="vue logo" src="../assets/vue_logo.png">
    <img alt="apollo logo" src="../assets/apollo_logo.png">
    <img alt="graphql logo" src="../assets/graphql_logo.png">
    <img alt="prisma logo" src="../assets/prisma_logo.png">

    <div id="nav">
        <router-link to="/">Home</router-link> |
        <router-link to="/about">About</router-link>
    </div>

  </div>
</template>

<style lang="css" scoped>
.my-header {
    position: fixed;
    left: 0;
    top: 0;
    width: 100%;
    color: white;
    background-color: gray;
    text-align: center;
}
img {
    width: 70px;
    height: 70px;
}
#nav {
    color: #d0d0d0;
    padding: 30px;
}

#nav a {
    font-weight: bold;
    color: #d0d0d0;
}
#nav a:hover {
    color: white;
}

#nav a.router-link-exact-active {
    color: #0a0a0a;
    text-decoration: none;
    cursor: default;
}
</style>
