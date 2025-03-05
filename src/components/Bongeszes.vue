<script setup>
import axios from 'axios';
import { onMounted, ref } from 'vue';
    const receptek = ref([]);
    const selectedRecept = ref({});
    const showReszeletek = ref(false);
    const getReceptek = async () => {
        try {
            const response = await axios.get('http://localhost/api/recept');
            receptek.value = response.data;
        } catch (error) {
            console.error(error);
        }
    }
    const getRecept = async (id) => {
        try {
            const response = await axios.get('http://localhost/api/recept',{
                params:{
                    id:id
                }
            });
            selectedRecept.value = response.data;
            console.log(response);
            showReszeletek.value = true;
        } catch (error) {
            console.error(error);
        }
    }
    onMounted(()=>{
        getReceptek();
    })
</script>
<template>
    <h2 class="text-warning">Receptek böngészése</h2>
    <ul class="list-group ">
        <li class="list-group-item d-flex align-items-center justify-content-between" v-for="recept in receptek">{{ recept.nev }}        <button class="btn btn-warning" @click="getRecept(recept.id)">Megtekintés</button>        </li>
    </ul>
    <div class="card mt-4 p-3" v-if="showReszeletek">
        <h1>{{ selectedRecept.nev }}</h1>
        <p><b>Elkészítési idő:</b> {{selectedRecept.ido}} perc</p>
        <p><b>Nehézség:</b> {{ selectedRecept.nehezseg }}</p>
        <p><b>Leírás:</b> {{ selectedRecept.leiras }}</p>
        <h3>Hozzávalók</h3>
        <ul>
            <li v-for="hozzavalo in selectedRecept.hozzavalok">
                {{ hozzavalo.nev }} - {{ hozzavalo.mennyiseg }} {{ hozzavalo.mertekegyseg }}
            </li>
        </ul>
    </div>
</template>