<script setup>

import { ref, reactive, computed, onMounted, nextTick } from 'vue'

const $input = ref(null)
const $output = ref(null)

const profile = Intl.DateTimeFormat().resolvedOptions()

const state = reactive({
  input: '',
  locale: profile.locale,
  dateStyle: 'short',
  timeStyle: 'short',
  timeZone: profile.timeZone
})

const output = computed(() => {
  const { input, locale, dateStyle, timeStyle, timeZone } = state
  const options = { dateStyle, timeStyle, timeZone }
  if (!input) return '<div class="text-gray-300">Output Locale</div>'
  const value = input.toLowerCase() === 'now'
    ? Date.now()
    : input
  try {
    const string = new Date(value).toLocaleString(locale, options)
    if (string === 'Invalid Date') throw Error('Invalid Date')
    return string
  } catch (e) {
    return `<div class="text-red-300">${e.message}</div>`
  }
})

onMounted(() => {
  const params = new URLSearchParams(window.location.search)
  state.input = params.get('i') || state.input
  state.locale = params.get('l') || state.locale
  state.dateStyle = params.get('ds') || state.dateStyle
  state.timeStyle = params.get('ts') || state.timeStyle
  state.timeZone = params.get('tz') || state.timeZone
  state.input
    ? nextTick(selectOutput)
    : $input.value.focus()
})

const selectOutput = () =>
  selectNode($output.value)

const selectNode = (node) => {
  const selection = window.getSelection()
  const range = document.createRange()
  range.selectNodeContents(node)
  selection.removeAllRanges()
  selection.addRange(range)
}

</script>

<template>
  <div class="flex flex-col items-center justify-center w-screen h-screen p-3 space-y-5 sm:p-10 md:p-0">
    <div class="text-xl">📆</div>
    <input ref="$input" tabindex="0" v-model="state.input" type="text" class="w-full font-mono text-lg text-center border-gray-400 rounded-md shadow-sm md:w-3/4 xl:w-1/2" placeholder="Input Date" />
    <div class="text-xl">↓</div>
    <div ref="$output" tabindex="0" v-html="output" @focus="selectOutput" class="w-full font-mono text-lg text-center border-gray-300 border-dashed select-all focus:border-x-red-300 form-input md:w-3/4 cursor-copy xl:w-1/2" />
    <div class="flex flex-col justify-center w-full pt-3 space-x-0 space-y-3 text-gray-500 sm:flex-row sm:space-y-0 sm:space-x-3 md:w-3/4 xl:w-1/2">
      <label class="text-xs">
        <span class="text-gray-500">Date Style</span>
        <select tabindex="0" v-model="state.dateStyle" class="block w-full mt-1 text-sm border-gray-300 rounded-md shadow-sm form-select">
          <option value="full">full</option>
          <option value="long">long</option>
          <option value="medium">medium</option>
          <option value="short">short</option>
        </select>
      </label>
      <label class="text-xs">
        <span class="text-gray-500">Time Style</span>
        <select tabindex="0" v-model="state.timeStyle" class="block w-full mt-1 text-sm border-gray-300 rounded-md shadow-sm form-select">
          <option value="full">full</option>
          <option value="long">long</option>
          <option value="medium">medium</option>
          <option value="short">short</option>
        </select>
      </label>
      <label class="text-xs">
        <span class="text-gray-500">Locale</span>
        <input tabindex="0" v-model="state.locale" type="text" class="block w-full mt-1 text-sm border-gray-300 rounded-md shadow-sm" placeholder="Locale" />
      </label>
      <label class="text-xs">
        <span class="text-gray-500">Time Zone</span>
        <input tabindex="0" v-model="state.timeZone" type="text" class="block w-full mt-1 text-sm border-gray-300 rounded-md shadow-sm" placeholder="Time Zone" />
      </label>
    </div>
  </div>
</template>

<style scoped>

input:focus::placeholder {
  color: transparent;
}

</style>
