<script setup>
import { ref } from 'vue';

    const hozzavalok = ref([
        {'id':1,'nev':'Liszt','mertekegyseg':'g'},
        {'id':2,'nev':'Cukor','mertekegyseg':'g'},
        {'id':3,'nev':'Só','mertekegyseg':'g'},
        {'id':4,'nev':'Víz','mertekegyseg':'ml'},
        {'id':5,'nev':'Tojás','mertekegyseg':'db'},
        {'id':6,'nev':'Olaj','mertekegyseg':'ml'},
    ]);
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
</script>
<template>
    <div class="mb-2">
        <label for="nev" class="form-label">Név</label>
        <input type="text" name="" id="nev" class="form-control">
    </div>
    <div class="mb-2">
        <label for="elkeszites" class="form-label">Elkészítési idő (perc)</label>
        <input type="text" name="" id="elkeszites" class="form-control">
    </div>
    <div class="mb-2">
        <label for="nehezseg" class="form-label">Nehézség</label>
        <select name="" id="nehezseg" class="form-select">
            <option value="Könnyű">Könnyű</option>
            <option value="Közepes">Közepes</option>
            <option value="Nehéz">Nehéz</option>
        </select>
    </div>
    <div class="mb-2">
        <label for="utmutato" class="form-label">Elkészítési útmutató</label>
        <textarea name="" id="utmutato" class="form-control"></textarea>
    </div>
    <div class="mb-2 d-flex align-items-center gap-2">
        <span>Hozzávalók</span>
        <button class="btn btn-warning">+</button>
    </div>
    <div class="mb-2">
        <div class="input-group mb-3" v-for="(item,index) in inputs">
            <select name="" id="" class="form-select" v-model="item.id" @change="changeMertekegyseg(index)">
                <option v-for="hozzavalo in hozzavalok" :value="hozzavalo.id">{{ hozzavalo.nev }}</option>
            </select>
            <input type="number" name="" id="" class="form-control" v-model="item.mennyiseg">
            
            <span class="input-group-text">{{ item.mertekegyseg }}</span>
            <button class="btn btn-danger" type="button" id="button-addon2">X</button>
        </div>
    </div>
</template>