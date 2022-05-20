<template>
  <div id="g-recaptcha" :data-size="invisible ? 'invisible': false" :data-sitekey="sitekey" :style="addMarginForRecaptcha2"/>
</template>

<script>
export default {
  props: {
    sitekey: {
      type: String,
      required: true,
    },
    invisible: {
      type: Boolean,
      default:false
    },
  },
  computed:{
    addMarginForRecaptcha2(){
      if(!this.invisible){
        return "display:flex;justify-content: center;margin: 20px 0;"  
      }
      return "";
    }
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