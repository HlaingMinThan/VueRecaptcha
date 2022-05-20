<template>
  <div id="app">
    <form
      action=""
      @submit.prevent="submit"
      style="max-width: 600px; margin: auto"
    >
      <input type="text" placeholder="email" v-model="email" />
      <input type="text" placeholder="password" v-model="password" />
      <VueRecaptcha
        @callback="callback"
        ref="recaptcha"
        sitekey="6LfY2-YfAAAAAMohJHhdVnaE02hV0GnOd-QHGNVg"
      />
      <button type="submit">submit</button>
    </form>
  </div>
</template>

<script>
import VueRecaptcha from "./components/VueRecaptcha";
export default {
  name: "App",
  components: {
    VueRecaptcha,
  },
  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    submit() {
      this.$refs.recaptcha.execute();
      console.log("hello world");
    },
    callback(token) {
      console.log(token);
    },
  },
};
</script>

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
