<template>
  <div id="app">
    <NavBar />
    <div id="content">
      <h1>Summarize any scientific paper</h1>
      <TextInput @changeState="state = $event" @showSummary="data = $event"/>
      <div id="result">
      <b-icon
        v-if="state === 'loading'"
        icon="arrow-clockwise"
        animation="spin"
        font-scale="4"
      ></b-icon>
      <SummarizationAccordion v-if="state === 'loaded'" :summaryItem="data"/>
      <b-alert v-if="state === 'error'" show variant="danger" dismissible>There was an error</b-alert>
      </div>
    </div>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import SummarizationAccordion from "./components/SummarizationAccordion.vue";
import NavBar from "./components/NavBar.vue";
import TextInput from "./components/TextInput.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
    SummarizationAccordion,
    NavBar,
    TextInput,
  },
  data() {
    return {
      state: "prev",
      data: {"final_summary": "Hola", "summaries":["Hola","muy","buenas"]}
    };
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
}

#content {
  margin: 30px 60px;
}

#result {
  margin: 40px 0px;
}
</style>
