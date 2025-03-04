<script setup>
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
</template>