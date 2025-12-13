<script setup lang="ts">
import { ref, computed } from 'vue'
import {options} from './options'
import {isIpValid,getNetworkAdress,getAddressesCount} from './functions'
import { UiButton, UiInput, UiSelect} from 'is323-km-components'

const ip = ref('')
const mask = ref(options[0])
const isShowResult = ref(false)

const NetworkAdress = computed(() => getNetworkAdress(ip.value,mask.value))

function showResult(){
  isShowResult.value = true
}
</script>

<template>
  <form @submit.prevent="showResult" class="form">
      <UiInput v-model="ip" />
      <UiSelect v-model="mask" :options="options" />
      <UiButton :disabled="!isIpValid(ip)" type="submit">Рассчитать</UiButton>
  </form>

  <div v-if="isShowResult && isIpValid(ip)" class="result">
    <div>IP адрес: {{ip}}</div>
    <div>Маска подсети: {{mask}}</div>
    <div>Адрес сети: {{NetworkAdress}}</div>
    <div>Кол-во адресов: {{getAddressesCount(mask)}}</div>
  </div>
  </template>

  <style>
  .form{
    display: flex;
    gap: 5px
  }
  .result{
    border-radius: 16px;
    padding: 16px;
    margin-top: 16px;
    font-size: 24px;
    width: 400px;
  }
  </style>




