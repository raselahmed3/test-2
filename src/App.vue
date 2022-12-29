<template>
  <div class="min-h-screen bg-gray-100">
    <div class="container py-6">
      <div class="bg-white p-4 shadow rounded">
        <div class=" flex -mx-4 items-center mb-6">
           <div class="flex-1 px-4">
           <select @change="getSpecificSura" class="quran-input" name="" id="">
              <option value=""> Select Sura</option>
              <option v-for="sura in suras" :value="sura.number">{{sura.name}} {{sura.englishName}}</option>
              </select>
          </div>
        <div class="flex-1 px-4 text-center">
          <h3 class="font-bold mb-1 text-lg">{{currentSura.englishName}}</h3>
            <p> {{currentSura.name}}</p>
        </div>
      <div class="flex-1 px-4">
        <select class="quran-input" name="" id="">
          <!-- <option value=""> Ayah</option> -->
          <option value="">Ayah {{currentSura.numberOfAyahs}}</option>
          </select>
      </div>
        </div>
        <div class="text-4xl text-center">
          <p class="flex item-center" v-if="currentSura.hasOwnProperty('ayahs')" v-for="ayah in currentSura.ayahs"> <span class="flex text-xl w-7 h-7 item-center justify-center border rounded-full mr-4">{{ayah.number}}</span>{{ayah.text}}</p>
        </div>
      </div>
    </div>
  </div>
  


  
</template>

<script >
import axios from 'axios';
export default {
  name: 'App',
  data() {
        return {
          suras: [],
            currentSura: [],
        }
    },
  mounted(){
  axios.get('https:////api.alquran.cloud/v1/surah')
  .then(response => {
    this.suras = response.data.data

  })
    this.querySpecificSura(1);
  },
  methods: {
    getSpecificSura(e) {
      this.querySpecificSura(e.target.value);
    },
    querySpecificSura(suraNumber) {
      axios.get('https:////api.alquran.cloud/v1/surah/' + suraNumber)
    .then(response => {
    this.currentSura = response.data.data

  })
    }
  }

};





</script>
