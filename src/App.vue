<template>
  <Dashpage>
  </Dashpage>
</template>

<script>
//import af tailwind CSS
import './assets/tailwind.css'
//import af dash_page komponent
import Dashpage from "./components/Dash_page.vue";
import { defineComponent } from 'vue';


export default defineComponent({
  name: 'App',
  components: {
    Dashpage
  },
  data() {
    return {}
  },

  methods: {}
});
</script>
