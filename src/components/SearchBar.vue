<script setup lang="ts">
// use store
import { useIpStore } from '~/store/ip'
// use functions os store
const { storeIP } = useIpStore()
// use data of store
const validIP = useIpStore()
// get validation situation from store
const isIpValid = ref()
// update validation situation from store (in the start of app and after any changes)
watchEffect(() => {
  isIpValid.value = validIP.ipValidation
})

// store input while typing (two way binding)
const enteredIp = ref('')

// call storeIP function of store and clear the input felid
function submitInput() {
  storeIP(enteredIp.value)
  enteredIp.value = ''
}
</script>

<template>
  <!-- Search Section -->
  <div
    absolute
    z-3
    top-0
    bottom-0
    left-0
    right-0
    mx-auto
    mt-auto
    h-15
    bg-teal-700
    sm:mb-5
    sm:w="60%"
    sm:rounded-2
    md:w="50%"
    lg:w="40%"
    xl:w="35%"
    class="2xl:w-35%"
  >
    <!-- Search Container (Input and Button) -->
    <div
      flex
      mx-auto
      my-auto
      justify-center
      w="90%"
      h="100%"
      sm:w="100%"
    >
      <!-- Input Section -->
      <input
        id="ip_address"
        v-model="enteredIp"
        type="text"
        name="ip_address"
        placeholder="Enter a valid IP address"
        h-10
        my-auto
        text="4.5"
        sm:text-5
        px-3
        rounded-l-2
        bg-stone-300
        shadow-inner
        w="80%"
        sm:w="85%"
        md:w="87%"
        focus:outline-none
        focus:bg-stone-200
        text-teal-900
        :class="(isIpValid) ? 'placeholder-teal-800/40' : 'placeholder-red'"
        placeholder-text="3.4"
        sm:placeholder-text="4.5"
        @keyup.enter="submitInput()"
      >
      <!-- Search Button -->
      <button
        h="10"
        w-10
        bg-zinc-900
        rounded-r-2
        my-auto
        shadow-inner
        text-5
        hover:text-6
        active:text="6.5"
        transition="all"
        duration="50"
        @click="submitInput()"
      >
        <!-- Button Icon -->
        <div
          i-carbon-search
          mx-auto
          my-auto
          text-stone-200
        />
      </button>
    </div>
  </div>
</template>
