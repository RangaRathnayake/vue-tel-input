<template>
  <div style="width: 50%; margin: auto;">
    <vue-tel-input v-model="phone" v-bind="bindProps"></vue-tel-input>
  </div>
</template>

<script>
import { ref } from 'vue';
import { VueTelInput } from 'vue-tel-input'
export default {
  name: 'App',
  components: {
    VueTelInput,
  },
  setup() {
    const phone = ref(null);

    return {
      phone: phone,
      bindProps: {
        mode: "international",
        defaultCountry: "LK",
        autoFormat: true,
        dropdownOptions: {
          showDialCodeInSelection: true,
          showSearchBox: true,
          showFlags: true
        }
      }
    }
  }
}

</script>

<style>
@import "https://unpkg.com/vue-tel-input@8.3.1/dist/vue-tel-input.css";
</style>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
