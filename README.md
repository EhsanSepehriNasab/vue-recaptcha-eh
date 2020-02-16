# Captcha validation on Vue.js module

## Features
* Validation user
* Change temp
* Validate captcha code in realtime

| Image  |
| --- |
| ![desktop](http://s7.picofile.com/file/8388282850/recaptcha.png)|



## Getting started
### Download
```
$ npm install vue-recaptcha-eh
```

### Usage
### ES6 modules
```
import VueRecaptchaEh from "../src/vue-recaptcha-eh";

```

### Vue file
```
import VueRecaptchaEh from '/path/to/vue-recaptcha-eh.vue';
```

## Example
```js
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

```

## Options
| Options | Type | Description | Default |
|:--|:--|:--|:--|
| invalidColor | String | border color input when code is valid | 'red' |
| validColor | String | border color input when code is invalid | 'green'  |
| textColor | String | ordinary text color| black |
| font | String | wave height | 17px "HiraKakuProN-W4-AlphaNum" |
| placeholder |  String | placeholder on empty | Please Enter Code |


## Callback

### **getValidation(target)**

##### Argument

* target : Boolean

| Values | Type | Description |
|:--|:--|:--|
|target|Boolean|true = Valid code & false = Invalid code|


## Quick Start
```
git clone https://github.com/EhsanSepehriNasab/vue-recaptcha-eh
cd vue-recaptcha-eh
npm install
vue serve example/App.vue
```

## License
**[MIT](https://github.com/mitsuyacider/vue-hashtag-textarea/blob/master/LICENSE.txt)**