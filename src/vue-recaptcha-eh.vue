<template>
  <div>
    <div class="headValideta">
      <div class="ValidetaEh LeftsideValideta">
        <div id="captcha"></div>
      </div>
      <button class="buttonValidetaEh" @click="makeCaptcha">↺</button>
      <div class="LeftsideValideta ">
        <input
          v-if="validCaptcha == false"
          @input="valideteMadeCaptcha"
          type="text"
          class="inputValidetaEh"
          :placeholder="option.placeholder"
          v-bind:style="{
            borderStyle: 'solid',
            color: option.textColor,
            borderColor: option.inValidColor,
            borderSize: '2px',
            font: option.font
          }"
          id="cpatchaTextBox"
        />
        <input
          v-if="validCaptcha == true"
          @input="valideteMadeCaptcha"
          type="text"
          class="inputValidetaEh"
          :placeholder="option.placeholder"
          v-bind:style="{
            borderStyle: 'solid',
            color: option.textColor,
            borderColor: option.validColor,
            borderSize: '2px',
            font: option.font
          }"
          id="cpatchaTextBox"
        />
      </div>
    </div>
  </div>
</template>

<style lang="scss">
.inputValidetaEh {
  padding: 12px 20px;
  display: inline-block;
  border: 1px solid #ccc;
  box-sizing: border-box;
}
.ValidetaEh {
  display: inline-block;
  border: 1px solid #ccc;
  box-sizing: border-box;
}
.LeftsideValideta {
  float: left;
}
.headValideta {
  width: 100%;
}
.buttonValidetaEh {
  float: left;
  font-size: 20px;
  text-align: center;
  background: none;
  box-shadow: none;
  border-radius: 0px;
  padding: 9px 15px;
  display: inline-block;
  border: 1px solid #ccc;
  box-sizing: border-box;
}
.buttonValidetaEh:focus {
  background: none;
  outline: none;
  padding: 9px 15px;
  display: inline-block;
  border: 1px solid #ccc;
  box-sizing: border-box;
}

.buttonValidetaEh:hover {
  background: none;
  outline: none;
  box-shadow: none;
  padding: 9px 15px;
  display: inline-block;
  border: 1px solid #ccc;
  box-sizing: border-box;
}

canvas {
  /*prevent interaction with the canvas*/
  pointer-events: none;
}
</style>

<script>
export default {
  name: "VueRecaptchaEh",
  props: {
    option: {
      type: Object
    }
  },
  data() {
    return {
      validCaptcha: false,
      defaultOption: {
        placeholder: "please Enter Code",
        textColor: "black",
        font: '17px "HiraKakuProN-W4-AlphaNum"',
        validColor: "green",
        inValidColor: "#E52B50"
      }
    };
  },
  created() {
    // NOTE: Set default option if not existence in props
    for (let key in this.defaultOption) {
      const value = this.option[key];
      if (value === undefined) {
        this.option[key] = this.defaultOption[key];
      }
    }
  },
  mounted() {
    this.createCaptcha();
  },
  computed: {
    createCaptcha: function() {
      this.makeCaptcha();
    },
    validateCaptcha: function() {
      this.valideteMadeCaptcha();
    }
  },
  mounted: function() {
    this.makeCaptcha();
  },
  methods: {
    makeCaptcha: function() {
      //clear the contents of captcha div first
      this.validCaptcha = false;
      document.getElementById("captcha").innerHTML = "";
      var charsArray =
        "0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ@!#$%^&*";
      var lengthOtp = 6;
      var captcha = [];

      for (var i = 0; i < lengthOtp; i++) {
        //below code will not allow Repetition of Characters
        var index = Math.floor(Math.random() * charsArray.length + 1); //get the next character from the array
        if (captcha.indexOf(charsArray[index]) == -1)
          captcha.push(charsArray[index]);
        else i--;
      }

      var canv = document.createElement("canvas");

      canv.id = "captcha";
      canv.width = 100;
      canv.height = 40;
      var ctx = canv.getContext("2d");
      ctx.font = "25px Georgia";
      ctx.strokeText(captcha.join(""), 0, 30);
      ctx.beginPath();
      ctx.moveTo(Math.random() * 100, Math.random() * 40);
      ctx.lineTo(Math.random() * 100, Math.random() * 40);
      ctx.strokeStyle = "#000000";
      ctx.lineWidth = 1;
      ctx.stroke();
      ctx.beginPath();
      ctx.moveTo(Math.random() * 100, Math.random() * 50);
      ctx.lineTo(Math.random() * 100, Math.random() * 50);
      ctx.strokeStyle = "#000000";
      ctx.lineWidth = 1;
      ctx.stroke();
      ctx.beginPath();
      ctx.moveTo(Math.random() * 100, Math.random() * 50);
      ctx.lineTo(Math.random() * 100, Math.random() * 50);
      ctx.strokeStyle = "#000000";
      ctx.lineWidth = 1;
      ctx.stroke();
      ctx.beginPath();
      ctx.moveTo(Math.random() * 100, Math.random() * 50);
      ctx.lineTo(Math.random() * 100, Math.random() * 50);
      ctx.strokeStyle = "#000000";
      ctx.lineWidth = 1;
      ctx.stroke();
      this.code = captcha.join("");
      document.getElementById("captcha").appendChild(canv); // adds the canvas to the body element
      this.$emit("getValidation", this.validCaptcha);
    },
    valideteMadeCaptcha: function() {
      if (document.getElementById("cpatchaTextBox").value == this.code) {
        this.validCaptcha = true;
      } else {
        this.validCaptcha = false;
      }
      this.$emit("getValidation", this.validCaptcha);
    }
  }
};
</script>
