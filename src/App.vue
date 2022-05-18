<template>
  <div id="app">
    <form action="" @submit.prevent="submit">
      <input type="text" placeholder="email" v-model="email" />
      <input type="text" placeholder="password" v-model="password" />
      <div
        id="g-recaptcha"
        data-size="invisible"
        :data-sitekey="sitekey"
      ></div>

      <button type="submit">submit</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      email: "",
      password: "",
      sitekey: "6LfY2-YfAAAAAMohJHhdVnaE02hV0GnOd-QHGNVg",
    };
  },
  methods: {
    getToken(token) {
      this.reset();
      console.log(token);
    },
    reset(){
      window.grecaptcha.reset();
    },
    submit() {
      window.grecaptcha.execute();
    },
    render() {
      setTimeout(() => {
        if (
          typeof window.grecaptcha === "undefined" ||
          typeof window.grecaptcha.render === "undefined"
        ) {
          this.render();
        } else {
          window.grecaptcha.render("g-recaptcha", {
            sitekey: this.sitekey,
            callback: (token) => {
              this.getToken(token);
            },
            // "expired-callback": this.expired,
          });
        }
      }, 100);
    },
  },
  mounted() {
    this.render();
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
