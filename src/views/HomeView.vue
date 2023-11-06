<script setup>
  import {ref} from 'vue' 
  const perhitungannilai = ref('')
  const perhitunganelemen = ref(['C', '*', '/', '-', 7, 8, 9, '+', 4, 5, 6, '%', 1, 2, 3, '=', 0, '.' ])
  const operasi = ref(null)
  const sebelumnilai = ref('')

  function action(ele){
    if(!isNaN(ele) || ele === "."){
      this.perhitungannilai += ele + ''
    }
    if(ele === "C"){
      this.perhitungannilai = ''
    }
    if(ele === '%'){
      this.perhitungannilai = this.perhitungannilai / 100;
    }
    if(['*', '/', '-', '+'].includes(ele)){
      this.operasi = ele
      this.sebelumnilai = this.perhitungannilai
      this. perhitungannilai = ''
    }
    if(ele === '='){
      this.perhitungannilai = eval(
        this.sebelumnilai + this.operasi + this.perhitungannilai
      ) 
      this.operasi = null
      this.sebelumnilai = ''
    }
  }
</script>
<template>
<div class="bg-[#234] max-w-[450px] p-6 mx-auto mt-5 shadow-2xl shadow-slate-650">
<div class="w-full bg-slate-500 p-4 shadow-md shadow-slate-900 text-right text-white font-normal text-xl">
  {{ perhitungannilai || 0 }}
</div>
<div class="grid grid-cols-4 gap-3 mt-4">
  <div class="" v-for="ele in perhitunganelemen" :key="ele">
    <div class="p-7 bg-slate-700 hover:bg-slate-900 transition-all duration-200 text-white text-center font-medium text-md cursor-pointer"
      :class="{'bg-red-400 hover:bg-gray-700': ['C', '*', '/', '-', '%', '+', '='].includes(ele)}"
      @click="action(ele)">
      {{ ele }}
    </div>
  </div>
</div>
</div>
</template>
<style scoped>
</style>