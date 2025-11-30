<script setup lang="ts">
import { ref, computed } from 'vue'
import { UiButton, UiSelect, UiInput, UiField } from 'my-blueside-ui-sanya'
import { SUBNET_MASK_OPTIONS } from '../constants/subnetMasks'
import { isIpValid } from '../utils/ipValidation'
import { getNetworkAddress, getAddressesCount } from '../utils/networkCalculations'

const ip = ref<string>('')
const mask = ref<string>('255.255.255.0')
const isShowResult = ref<boolean>(false)

const isIpCorrect = computed(() => isIpValid(ip.value))

const handleSubmit = () => {
  if (isIpCorrect.value) {
    isShowResult.value = true
  }
}

const handleKeyup = (e: KeyboardEvent) => {
  if (e.key === 'Enter') {
    handleSubmit()
  }
}
</script>

<template>
  <div class="ip-calculator">
    <h1 class="title">Калькулятор подсетей</h1>

    <div class="form-card">
      <form @submit.prevent="handleSubmit">
        <UiInput
          v-model="ip"
          class="input-full"
          @keyup="handleKeyup"
        />
        <UiSelect
          v-model="mask"
          :options="SUBNET_MASK_OPTIONS"
          class="select-full"
        />
        <UiButton
          @click="handleSubmit"
          :disabled="!isIpCorrect"
          class="button-full"
        >
          Рассчитать
        </UiButton>
      </form>
    </div>

    <div v-if="isShowResult && isIpCorrect" class="result-card">
      <UiField label="IP-адрес" class="result-field">{{ ip }}</UiField>
      <UiField label="Маска подсети" class="result-field">{{ mask }}</UiField>
      <UiField label="Адрес сети" class="result-field">{{ getNetworkAddress(ip, mask) }}</UiField>
      <UiField label="Количество хостов" class="result-field">{{ getAddressesCount(mask) }}</UiField>
    </div>
  </div>
</template>

<style scoped>
.ip-calculator {
  padding: 2rem;
  max-width: 700px;
  margin: 0 auto;
}

.title {
  text-align: center;
  font-size: 1.75rem;
  font-weight: 600;
  margin-bottom: 1.5rem;
  color: #ef7cfa;
}

.form-card {
  background-color: rgba(0, 0, 0, 0.05);
  border-radius: 12px;
  padding: 1.5rem;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.05);
  margin-bottom: 2rem;
}

.input-full,
.select-full,
.button-full {
  width: 100%;
  margin-bottom: 1rem;
}

.result-card {
  background-color: rgba(0, 0, 0, 0.05);
  border: 1px solid  #ff00ff;
  border-radius: 12px;
  padding: 1.5rem;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.05);
}

.result-field {
  margin-bottom: 1rem;
}

.result-field .ui-field__label {
  margin-bottom: 0.25rem;
}
</style>