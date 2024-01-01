<template>
  <div style="width: 50%; margin: auto;">
    <vue-tel-input v-model="phone" v-bind="bindProps" v-on:keyup="inputEvent($event)"
      @click="textClickEvent($event)"></vue-tel-input>
  </div>
  <!-- <div>
    <br>
    Tel: {{ phone }}<br>
    <br>
    before: {{ before }}<br>
    <br>
    positionChanged: {{ positionChanged }}<br>
  </div> -->
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
        autoFormat: false,
        dropdownOptions: {
          showDialCodeInSelection: true,
          showSearchBox: true,
          showFlags: true
        }
      }
    }
  },

  data() {
    return {
      before: 0,
      positionChanged: false,
    }
  },

  methods: {

    inputEvent(event) {
      if (this.bindProps.autoFormat) return;
      // console.log("defalut -> ", event.target.selectionStart);
      // console.log("key Code ", event.keyCode);
      if (event.keyCode == 37 || event.keyCode == 39) {
        this.before = event.target.selectionStart;
        this.positionChanged = true;
      } else if (event.keyCode > 48 && event.keyCode < 58) {
        if (this.positionChanged) {
          event.target.setSelectionRange(Number(this.before) + 1, Number(this.before) + 1);
          this.before = Number(this.before) + 1;
        }
      }
    },

    textClickEvent(event) {
      if (this.bindProps.autoFormat) return;
      // console.log("textClickEvent");
      // console.log(event.target.selectionStart);
      this.before = event.target.selectionStart;
      this.positionChanged = true;
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
