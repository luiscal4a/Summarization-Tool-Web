<template>
  <div id="container">
    <b-card title="Generated summary">
      <b-card-text>
        {{ summaryItem.final_summary }}
      </b-card-text>
      <b-button id = "success_btn" @click="showDismissibleAlert=true" variant="success">Rate positively
        <b-icon-arrow-up></b-icon-arrow-up>
      </b-button>
      <b-button href="#" variant="danger">Rate negatively
        <b-icon-arrow-down></b-icon-arrow-down>
      </b-button>
    </b-card>
    <b-alert
      variant="success"
      dismissible
      :show="showDismissibleAlert"
    >Thanks for the feedback!</b-alert>
    <hr>
    <div v-for="(iteration, index) in summaryItem.summaries" :key="index" style="margin-top:20px;">
      <h2 style="font-weight: bold;">Iteration {{ index + 1 }}</h2>
      <b-container fluid>
        <b-row cols="1" cols-sm="2" cols-md="3" cols-lg="3">
          <b-col
            v-for="(item, index2) in iteration"
            :key="item.message"
            col
            no-gutters
            class="mb-2"
          >
            <b-card>
              <b-card-title>Summary {{ index2 + 1 }}</b-card-title>
              <b-card-text>
                {{ item }}
              </b-card-text>
            </b-card>
          </b-col>
        </b-row>
      </b-container>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [
        { title: "Foo2", message: "Foo" },
        { title: "Bar2", message: "Bar" },
        { title: "Foo2", message: "Foo" },
        { title: "Bar2", message: "Bar" },
        { title: "Foo2", message: "Foo" },
        { title: "Bar2", message: "Bar" },
        { title: "Foo2", message: "Foo" },
        { title: "Bar2", message: "Bar" },
        { title: "Foo2", message: "Foo" },
        { title: "Bar2", message: "Bar" },
        { title: "Foo2", message: "Foo" },
        { title: "Bar2", message: "Bar" },
        { title: "Foo2", message: "Foo" },
        { title: "Bar2", message: "Bar" },
      ],
      colors: [],
      myStyle: {
        backgroundColor: "#16a085",
      },
      showDismissibleAlert: false
    };
  },

  props: {
    summaryItem: Object,
  },

  methods: {
    hex(c) {
      var s = "0123456789abcdef";
      var i = parseInt(c);
      if (i == 0 || isNaN(c)) return "00";
      i = Math.round(Math.min(Math.max(0, i), 255));
      return s.charAt((i - (i % 16)) / 16) + s.charAt(i % 16);
    },

    /* Convert an RGB triplet to a hex string */
    convertToHex(rgb) {
      return this.hex(rgb[0]) + this.hex(rgb[1]) + this.hex(rgb[2]);
    },

    /* Remove '#' in color hex string */
    trim(s) {
      return s.charAt(0) == "#" ? s.substring(1, 7) : s;
    },

    /* Convert a hex string to an RGB triplet */
    convertToRGB(hex) {
      var color = [];
      color[0] = parseInt(this.trim(hex).substring(0, 2), 16);
      color[1] = parseInt(this.trim(hex).substring(2, 4), 16);
      color[2] = parseInt(this.trim(hex).substring(4, 6), 16);
      return color;
    },

    generateColor(colorStart, colorEnd, colorCount) {
      // The beginning of your gradient
      var start = this.convertToRGB(colorStart);

      // The end of your gradient
      var end = this.convertToRGB(colorEnd);

      // The number of colors to compute
      var len = colorCount;

      //Alpha blending amount
      var alpha = 0.0;

      var saida = [];

      let i = 0;
      for (i = 0; i < len; i++) {
        var c = [];
        alpha += 1.0 / len;

        c[0] = start[0] * alpha + (1 - alpha) * end[0];
        c[1] = start[1] * alpha + (1 - alpha) * end[1];
        c[2] = start[2] * alpha + (1 - alpha) * end[2];

        saida.push("#" + this.convertToHex(c));
      }

      return saida;
    },
  },

  mounted() {
    this.colors = this.generateColor(
      "#28a745",
      "#166e2a",
      this.summaryItem.summaries.length
    );
    console.log(this.colors);
  },
};
</script>

<style scoped>
#title {
  text-align: left;
}

#success_btn {
  margin-right: 10px;
}
</style>