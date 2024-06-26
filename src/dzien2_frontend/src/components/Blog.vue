<template>
    <div>
        <h2 class="text-green-700">Wpisy na bloga:</h2>
        <div class="w-100 flex flex-row-reverse">
            <button @click="pobierzWpisy" class="bg-green-700 rounded text-white p-4">odśwież</button>
        </div>
        <div class="grid mx-6 gap-4 my-4">
        <div v-for="(wpis, index) in wpisy" class="grid drop-shadow-xl bg-stone-300 p-4">
            <p>id: {{ index }}</p>
            <p>{{ wpis }}</p>
            <button  class="bg-green-700 rounded text-white p-4" @click="deleteWpis(index)">usuń</button>
            </div>
        </div>
        <div class="flex justify-center flex-col">
        <input v-model="nowyBlog" class="border-2 border-blue-600 p-4" type="text">
        <button class="bg-green-700 rounded text-white p-4" @click="dodajWpisy">dodaj</button>
    </div>
    </div>
</template>

<script>
import { dzien2_backend } from 'declarations/dzien2_backend/index';

export default {
    data() {
        return {
            wpisy: [],
            nowyBlog: ""
        }
    },
    methods: {
        async dodajWpisy() {
            await dzien2_backend.dodaj_wpis(this.nowyBlog);
            await this.pobierzWpisy();
        },
        async deleteWpis(index) {
            await dzien2_backend.usun_wpis(index);
            await this.pobierzWpisy();
        },
        async pobierzWpisy() {
            this.wpisy = await dzien2_backend.odczytaj_wpisy();
        }
    },
    async mounted(){
        this.pobierzWpisy()
    }
}
</script>