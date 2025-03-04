<script setup>
import { ref } from 'vue';
    const receptek = ref([
        {'id':1,'nev':'Palacsinta'}
    ])
</script>
<template>
    <h2>Receptek böngészése</h2>
    <ul class="list-group ">
        <li class="list-group-item d-flex align-items-center justify-content-between" v-for="recept in receptek">{{ recept.nev }}        <button class="btn btn-warning">Megtekintés</button>        </li>
    </ul>
</template>