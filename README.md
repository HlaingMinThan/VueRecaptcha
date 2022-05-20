
# Vue Simple Recaptcha

a simple way to integrate google Recaptcha v2 in your vue2 project. 
Support for both of the invisible and box tick.





## Installation

add cdn link of google v2 recaptcha api in the head tag of index.html

```bash
<script src="https://www.google.com/recaptcha/api.js" async defer></script>
```

Install vue-simple-recaptcha with npm

```bash
npm i vue-simple-recaptcha
```
App.vue
```bash
<template>
  <div id="app">
    <form action="" @submit.prevent="submit">
      <input type="text" />
      <VueSimpleRecaptcha
        sitekey="..."
        ref="recaptcha"
        @callback="callback"
      />
      <button type="submit">Submit</button>
    </form>
  </div>
</template>

<script>
import VueSimpleRecaptcha from "vue-simple-recaptcha";

export default {
  name: "App",
  components: {
    VueSimpleRecaptcha,
  },
  methods: {
    callback(token){
      console.log(token)
      //make ajax request
      console.log('handling ajax request here')
    },
    submit() {
      this.$refs.recaptcha.execute()
    },
  },
};
</script>
```
## Props

invisible - Boolean (default - false)