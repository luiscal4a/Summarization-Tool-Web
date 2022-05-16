<template>
  <div>
    <b-form @submit.prevent="onSubmit()">
      <b-form-textarea
        id="textarea-rows"
        placeholder="Submit text to summarize"
        v-model="text"
        rows="12"
      ></b-form-textarea>
      <b-form-select
        v-model="selected"
        :options="options"
        class="mb-3"
        value-field="item"
        text-field="name"
      ></b-form-select>
      <b-row class="my-1">
        <b-col sm="3">
          <label for="input-none">Minimum token length:</label>
        </b-col>
        <b-col sm="9">
          <b-form-input
            v-model="min_len"
            placeholder="Enter your name"
            type="number"
            class="mb-3"
          ></b-form-input>
        </b-col>
      </b-row>
      <b-row class="my-1">
        <b-col sm="3">
          <label for="input-none">Maximum token length:</label>
        </b-col>
        <b-col sm="9">
          <b-form-input
            v-model="max_len"
            placeholder="Enter your name"
            type="number"
            class="mb-3"
          ></b-form-input>
        </b-col>
      </b-row>
      <b-button type="submit" variant="primary" id="submit-button"
        >Submit</b-button
      >
    </b-form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      text: "",
      selected: "prophetnet",
      min_len: 75,
      max_len: 300,
      options: [
        { item: "prophetnet", name: "Prophetnet whole document summarization" },
        { item: "distilbert", name: "Distilbert division summarization" },
      ],
    };
  },
  methods: {
    onSubmit(event) {
      this.holaMundo();
    },
    holaMundo() {
      let localThis = this;
      this.$emit("changeState", "loading");
      axios
        .post("http://127.0.0.1:8000/summarize/", {
          content: localThis.text,
          model: localThis.selected,
          min_length: localThis.min_len,
          max_length: localThis.max_len
        })
        .then((result) => {
          console.log(result.data);
          localThis.$emit("changeState", "loaded");
          localThis.$emit("showSummary", result.data);
        })
        .catch(function (error) {
          localThis.$emit("changeState", "error");
        });
    },
  },
};
</script>

<style>
#submit-button {
  width: 100%;
}
</style>