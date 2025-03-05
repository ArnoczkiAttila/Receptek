<script setup>
import axios from 'axios';
import { onMounted, ref } from 'vue';
    
    const recept = ref({
        nev:'',
        ido:0,
        nehezseg:'',
        leiras:''
    });
    const hozzavalok = ref([]);
    const inputs = ref([
        {'id':'','mennyiseg':0,'mertekegyseg':''}
    ]);
    const changeMertekegyseg = (index) => {
        hozzavalok.value.forEach(element => {
            if (inputs.value[index].id == element.id) {
                inputs.value[index].mertekegyseg = element.mertekegyseg;
                return;
            }
        });
    }
    const addHozzavalo = () => {
        inputs.value.push({'id':'','mennyiseg':0,'mertekegyseg':''});
    } 
    const deleteHozzavalo = (index) => {
        inputs.value.splice(index,1);
    } 
    const getHozzavalo = async () => {
        try {
            const response = await axios.get('http://localhost/api/hozzavalo');
            hozzavalok.value = response.data;
        } catch (error) {
            console.error(error);
        }
    }
    const addRecept = async () => {
        try {
            const response = await axios.post('http://localhost/api/recept',{
                'nev':recept.value.nev,
                'ido':recept.value.ido,
                'nehezseg':recept.value.nehezseg,
                'leiras':recept.value.leiras,
                'hozzavalok':inputs.value
            });
            recept.value = {
                nev:'',
                ido:0,
                nehezseg:'',
                leiras:''
            };
            inputs.value = [{'id':'','mennyiseg':0,'mertekegyseg':''}];
            console.log(response);
        } catch (error) {
            console.error(error);
        }
    }
    onMounted(()=>{
        getHozzavalo();
    })
</script>
<template>
    <h2 class="text-warning">Új recept hozzáadása</h2>
    <div class="mb-2">
        <label for="nev" class="form-label ">Név</label>
        <input type="text" name="" id="nev" v-model="recept.nev" class="form-control">
    </div>
    <div class="mb-2">
        <label for="elkeszites" class="form-label">Elkészítési idő (perc)</label>
        <input type="text" name="" v-model="recept.ido" id="elkeszites" class="form-control">
    </div>
    <div class="mb-2">
        <label for="nehezseg" class="form-label">Nehézség</label>
        <select name="" id="nehezseg" class="form-select" v-model="recept.nehezseg">
            <option value="Könnyű">Könnyű</option>
            <option value="Közepes">Közepes</option>
            <option value="Nehéz">Nehéz</option>
        </select>
    </div>
    <div class="mb-2">
        <label for="utmutato" class="form-label">Elkészítési útmutató</label>
        <textarea name="" id="utmutato" class="form-control" v-model="recept.leiras"></textarea>
    </div>
    <div class="mb-2 d-flex align-items-center gap-2">
        <span class="text-warning">Hozzávalók</span>
        <button class="btn btn-warning" @click="addHozzavalo">+</button>
    </div>
    <div class="mb-2">
        <div class="input-group mb-3" v-for="(item,index) in inputs">
            <select name="" id="" class="form-select" v-model="item.id" @change="changeMertekegyseg(index)">
                <option v-for="hozzavalo in hozzavalok" :value="hozzavalo.id">{{ hozzavalo.nev }}</option>
            </select>
            <input type="number" name="" id="" class="form-control" v-model="item.mennyiseg">
            
            <span class="input-group-text">{{ item.mertekegyseg }}</span>
            <button class="btn btn-danger" type="button" id="button-addon2" @click="deleteHozzavalo(index)">X</button>
        </div>
    </div>
    <div class="mb-2">
        <button class="btn btn-warning" @click="addRecept">
            Recept mentése
        </button>
    </div>
</template>