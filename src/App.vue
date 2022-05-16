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
        <SummarizationCards v-if="state === 'loaded'" :summaryItem="data" />
        <b-alert v-if="state === 'error'" show variant="danger" dismissible
          >There was an error</b-alert
        >
      </div>
    </div>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import SummarizationCards from "./components/SummarizationCards.vue";
import NavBar from "./components/NavBar.vue";
import TextInput from "./components/TextInput.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
    SummarizationCards,
    NavBar,
    TextInput,
  },
  data() {
    return {
      state: "prev",
      data: { 
        final_summary: "Long documents introduce a lot of noise to the summarization process. Large parts of the document are not really key to its narrative and thus should be ignored. By exploiting the structure of a document it is possible to scale to documents of arbitrary length such as review papers or financial reports. Instead of an RNN model we decided to use a Transformerbased model, since the computational complexity of full attention Transformers explode for very long sequences.", 
        summaries: [[
          "Summarizing long documents is a very different problem to newswire summarization. Long documents introduce a lot of noise to the summarization process. Large parts of the document are not really key to its narrative and thus should be ignored. Long summaries typically contain a number of diverse key information points. We show that our approach canenhance the ability of summarization models and lead to improved results.",
          "This paper is based on past work that assumed theexistence of structured summaries. Here we lift this assumption by using sentence level Rougesimilarities in order to match sentences of the summary with parts of the document. When paired with a very strong Transformer model such as PEGASUS, our method produces results that are on par with the state-ofthe-art on both datasets.",
          "Existing approaches for summarizing academic articles include extractive models that perform sentence selection and hybrid models that first select and thenre-write sentences from the full text. By exploiting the structure of a document it is possible to scale to documents of arbitrary length such as review papers or financial reports. A number of publicly available datasets of short articles are commonly used as a benchmark for many of the earlier summarization methods.",
          "We propose a divide-and-conquer approach for the summarization of long documents. Our approach assumes that long documents arestructured into discrete sections. Each section of the document is treated as a different example during the training of the model. Instead of an RNN model we decided to use a Transformerbased model, since the computational complexity and memory requirements of full attention Transformers explode for very long sequences."
          ],["Long documents introduce a lot of noise to the summarization process. Large parts of the document are not really key to its narrative and thus should be ignored. By exploiting the structure of a document it is possible to scale to documents of arbitrary length such as review papers or financial reports. Instead of an RNN model we decided to use a Transformerbased model, since the computational complexity of full attention Transformers explode for very long sequences."]] },
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
