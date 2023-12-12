<script setup lang="ts">
import { ref } from "vue";

const inputValue = ref("");
const result = ref();
const conversionType = ref("binaryToDecimal");

function convertBinary() {
  const value = inputValue.value;

  if (conversionType.value === "binaryToDecimal") {
    if (value) {
      result.value = parseInt(value, 2);
    }
  } else {
    if (value) {
      result.value = parseInt(value).toString(2);
    }
  }
}
</script>

<template>
  <div class="flex flex-col justify-center items-center mb-24">
    <h1 class="text-3xl text-center my-16 mx-auto">Binary Decimal Converter</h1>
    <form @submit.prevent="convertBinary()" class="max-w-sm mx-auto">
      <label
        for="types"
        class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
        >Pilih type konversi</label
      >
      <select
        v-model="conversionType"
        id="types"
        class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg mb-2 focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
      >
        <option value="binaryToDecimal">Binary To Decimal</option>
        <option value="decimalToBinary">Decimal To Binary</option>
      </select>

      <div class="mb-5">
        <label
          for="number"
          class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
          >Masukan Angka
          {{
            conversionType === "binaryToDecimal" ? "Binary" : "Desimal"
          }}</label
        >
        <input
          type="text"
          id="number"
          v-model="inputValue"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          :placeholder="conversionType === 'binaryToDecimal' ? '101' : '126'"
          :maxlength="conversionType === 'binaryToDecimal' ? 8 : ''"
          :pattern="conversionType === 'binaryToDecimal' ? '[01]+' : '[0-9]+'"
          required
        />
      </div>
      <button
        type="submit"
        class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
      >
        Ubah
      </button>
      <div
        v-if="result !== undefined"
        class="flex justify-center items-center max-w-sm p-2 my-4 bg-white border border-gray-200 rounded-lg shadow hover:bg-gray-100 dark:bg-gray-800 dark:border-gray-700 dark:hover:bg-gray-700"
      >
        <h5
          class="text-2xl font-bold tracking-tight text-gray-900 dark:text-white"
        >
          {{ result }}
        </h5>
      </div>
    </form>
  </div>
</template>
