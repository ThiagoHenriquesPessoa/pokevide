<script setup>

</script>

<template>
  <div class="main">
    <!-- NAVBAR -->
    <nav class="navbar navbar-expand-lg navbar-dark bg-primary">
      <div class="container-fluid">
        <router-link class="navbar-brand" to="/">
          <img src="https://cdn-icons-png.flaticon.com/512/188/188987.png" alt="Logo" width="30" height="24" class="d-inline-block align-text-top">
          Pokevite
        </router-link>      
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav">
            <li class="nav-item">
              <router-link class="nav-link" aria-current="page" to="/">Home</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="/about">About</router-link>
            </li>
          </ul>
        </div>
      </div>
    </nav>


    <!-- CONTENT -->  
    <router-view />
  </div>

  <footer class="bg-primary text-light">
    <div>
      Design in {{ new Date().getFullYear() }}
    </div>
  </footer>
</template>

<style>
body{
  background: rgb(2,0,36);
background: radial-gradient(circle, 
              rgba(2,0,36,1) 0%,
              rgb(15, 15, 85) 0%,
              rgba(159,239,255,1) 100%);
}
footer{
  position: fixed;
  bottom: 0;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 56px;
}
</style>
