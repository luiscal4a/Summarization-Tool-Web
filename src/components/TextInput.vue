<template>
  <div>
    <b-form @submit.prevent="onSubmit()">
      <b-form-textarea
        id="textarea-rows"
        placeholder="Submit text to summarize"
        v-model="text"
        rows="12"
      ></b-form-textarea>
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
    };
  },
  methods: {
    onSubmit(event) {
      this.holaMundo()
    },
    holaMundo() {
      let localThis = this
      this.$emit("changeState", "loading");
      axios.post("http://127.0.0.1:8000/summarize/", {
        content: localThis.text
      }).then((result) => {
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