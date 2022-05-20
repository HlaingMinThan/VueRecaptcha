<script>
import Vue from 'vue';
import VueSimpleRecaptcha from '@/vue-simple-recaptcha.vue';

export default Vue.extend({
  name: 'ServeDev',
  components: {
    VueSimpleRecaptcha
  }
});
</script>

<template>
  <div id="app">
    <vue-simple-recaptcha :sitekey="sitekey"/>
  </div>
</template>
<script>
export default {
  props: {
    sitekey: {
      type: String,
      required: true,
    },
  },
}
</script>
