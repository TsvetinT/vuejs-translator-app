
<template>
  <div class="text-center" id="app">
    <h1>Word Translator</h1>
    <translate-form  v-on:formSubmit="translateText"></translate-form>
    <hr>
    <translate-output v-text="translatedText"></translate-output>
  </div>
</template>

<script>
import translateForm from "./components/translateForm.vue";
import translateOutput from "./components/translateOutput.vue"
export default {
  name: "App",
  components: {
    "translate-form": translateForm,
    "translate-output":translateOutput
  },
  data: function(){
    return {
      translatedText:''
    }
  },
  methods: {
    translateText: function(text, language) {
      this.$http.get(
        'https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20180617T162900Z.063274634975c936.da9332ca8276845360f194f758d636cfd2186f48&lang='+language+'&text='+text
      ).then((response) => {
        this.translatedText = response.body.text[0];
      });
    }
  }
};
</script>


<style>
body {
  background:fefefe;
}
</style>
