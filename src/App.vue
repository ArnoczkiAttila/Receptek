<script setup>
  import Uj from './components/Uj.vue';
  import Bongeszes from './components/Bongeszes.vue';
  import { ref, shallowRef } from 'vue';

  const uj = Uj;
  const bongeszes = Bongeszes;
  const selectedComponent = shallowRef(uj);
</script>

<template>
  <div class="container-md">
    <nav class="navbar navbar-expand-md">
      <div class="container-fluid">
        <a class="navbar-brand" href="#"><img src="/logo.png" alt="" width="150px"></a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav mx-auto">
            <li class="nav-item mx-3">
              <button class="nav-link" :class="selectedComponent == uj?'active':''" @click="selectedComponent = uj">Új recept hozzáadása</button>
            </li>
            <li class="nav-item mx-3">
              <button class="nav-link" :class="selectedComponent == bongeszes?'active':''" @click="selectedComponent = bongeszes">Receptek böngészése</button>
            </li>
          </ul>
        </div>
      </div>
    </nav>

    <div class="row">
      <div class="col">
        <component :is="selectedComponent"/>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>
