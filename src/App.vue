<template>
  <div id="app">
    <NavBar />
    <div id="content">
      <h1>Summarize any scientific paper</h1>
      <TextInput @changeState="state = $event" @showSummary="data = $event" />
      <div id="result">
        <b-icon
          v-if="state === 'loading'"
          icon="arrow-clockwise"
          animation="spin"
          font-scale="4"
        ></b-icon>
        <SummarizationAccordion v-if="state === 'loaded'" :summaryItem="data" />
        <b-alert v-if="state === 'error'" show variant="danger" dismissible
          >There was an error</b-alert
        >
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
      data: { 
        final_summary: "A. Gidiotis is with the School of Informatics, Aristotle University of Thessaloniki, Greece . He and G. Tsoumakas propose a novel divideand-conquer approach that breaks both the document and its target summary into multiple smaller source-target pairs . They train a neural model that learns to summarize these smaller document parts, and then inferenceaggregates the partial summaries in order to produce a final complete summary .", 
        summaries: [
          "A. Gidiotis is with the School of Informatics, Aristotle University of Thessaloniki, Greece . He and G. Tsoumakas propose a novel divideand-conquer approach that breaks both the document and its target summary into multiple smaller source-target pairs . They then train a neural model that learns to summarize these smaller document parts, and then inferenceaggregates the partial summaries in order to produce a final complete summary .",
          "Using a 3 years-old sequence-to-sequence model, our approach manages to achieve surprisingly good results, surpassing recent more advanced models [14], [15] In addition, when paired with a very strong Transformer model such as PEGASUS, our method produces results that are on par with the state-ofthe-art on both datasets . This paper is based on past work that assumed the existence of structured summaries, such as those available for some of the biomedical articles indexed in PubMed ",
          "In cases where the input and target sequences are longer, the complexity of models that process the complete article at once increases dramatically making such methods infeasible . Different approaches attempt to solve this problem by exploiting the structure of a document . We treat each section of the text as a separate “summarization instance” and as a result our method is easily parallelizable . We use a Pre-training with Extracted Gap-sentences for Abstractive SUmmarization Sequence-to-sequence (PEGASUS) model .",
          "A. Gidiotis is with the School of Informatics, Aristotle University of Thessaloniki, Greece . He and G. Tsoumakas propose a novel divideand-conquer approach that breaks both the document and its target summary into multiple smaller source-target pairs . They train a neural model that learns to summarize these smaller document parts, and then inferenceaggregates the partial summaries in order to produce a final complete summary ."] },
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
