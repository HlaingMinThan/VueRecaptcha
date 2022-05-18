<template>
  <div id="g-recaptcha" data-size="invisible" :data-sitekey="sitekey"></div>
</template>

<script>
export default {
  data() {
    return {
      sitekey: "6LfY2-YfAAAAAMohJHhdVnaE02hV0GnOd-QHGNVg",
    };
  },
  methods: {
    getToken(token) {
      this.$emit('callback',token);
      this.reset();
    },
    reset() {
      window.grecaptcha.reset();
    },
    execute(){
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
</style>