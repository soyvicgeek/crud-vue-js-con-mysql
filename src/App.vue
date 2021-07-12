<template>
  <nav class="navbar navbar-expand navbar-light bg-light">
      <div class="nav navbar-nav">

          <router-link to="/listar" class="nav-link">Listar</router-link>
          <router-link to="/crear" class="nav-link">Crear</router-link>

      </div>
  </nav>
  <br><br>
  <router-view/>
</template>