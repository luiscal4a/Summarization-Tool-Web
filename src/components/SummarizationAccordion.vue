<template>
  <div id="container">
    <h2 id="title">Generated summary</h2>
    <p>{{summaryItem.final_summary}}</p>
    <div class="accordion" role="tablist">
      <b-card
        no-body
        class="mb-1"
        v-for="(item, index) in summaryItem.summaries"
        :key="item.message"
      >
        <b-card-header header-tag="header" class="p-1" role="tab">
          <b-button block v-b-toggle="'accordion-' + index" v-bind:style="{backgroundColor: colors[index]}">
            Summary {{index + 1}}
          </b-button>
        </b-card-header>
        <b-collapse
          :id="'accordion-' + index"
          accordion="my-accordion"
          role="tabpanel"
        >
          <b-card-body>
            <b-card-text>{{ item }} </b-card-text>
          </b-card-body>
        </b-collapse>
      </b-card>
    </div>

<!--
    <div v-for="(color, index) in colors" :key="index" v-bind:style="{backgroundColor: color}">COLOR "+cor+"° - #{{color}}</div>
 -->
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
      myStyle:{
            backgroundColor:"#16a085" 
            }
    };
  },

  props: {
    summaryItem: Object
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

    let i = 0
      for (i = 0; i < len; i++) {
        var c = [];
        alpha += 1.0 / len;

        c[0] = start[0] * alpha + (1 - alpha) * end[0];
        c[1] = start[1] * alpha + (1 - alpha) * end[1];
        c[2] = start[2] * alpha + (1 - alpha) * end[2];

        saida.push("#"+this.convertToHex(c));
      }

      return saida;
    },
  },

  mounted() {
      this.colors = this.generateColor('#28a745','#166e2a',this.summaryItem.summaries.length);
      console.log(this.colors)
  }
};
</script>

<style scoped>
#title {
  text-align: left;
}
</style>