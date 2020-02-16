<template>
  <vuerecaptchaeh v-on:getValidation="Validation" :option="option">
  </vuerecaptchaeh>
</template>

<script>
import VueRecaptchaEh from "../src/vue-recaptcha-eh";

export default {
  data() {
    return {
      option: {
        placeholder: "please Enter Code",
        textColor: "black",
        font: '17px "HiraKakuProN-W4-AlphaNum"',
        validColor: "green",
        inValidColor: "#E52B50"
      },
      validation: false
    };
  },
  methods: {
    Validation: function(target) {
      // target = true | false  it's mean a code is valid or invalid
      this.validation = target;
    }
  },
  components: {
    VueRecaptchaEh
  }
};
</script>
