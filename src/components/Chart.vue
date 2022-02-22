
<script>
import Chart from "chart.js";
import { generateChart } from "vue-chartjs";

Chart.defaults.multicolorLine = Chart.defaults.line;
Chart.controllers.multicolorLine = Chart.controllers.line.extend({
  draw: function (ease) {
    var startIndex = 0,
      meta = this.getMeta(),
      points = meta.data || [],
      colors = this.getDataset().colors,
      area = this.chart.chartArea,
      originalDatasets = meta.dataset._children.filter(function (data) {
        return !isNaN(data._view.y);
      });

    function _setColor(newColor, meta) {
      meta.dataset._view.borderColor = newColor;
    }

    if (!colors) {
      Chart.controllers.line.prototype.draw.call(this, ease);
      return;
    }
    for (var i = 2; i <= colors.length; i++) {
      if (colors[i - 1] !== colors[i]) {
        _setColor(colors[i - 1], meta);
        meta.dataset._children = originalDatasets.slice(startIndex, i);
        meta.dataset.draw();
        startIndex = i - 1;
      }
    }

    meta.dataset._children = originalDatasets.slice(startIndex);
    meta.dataset.draw();
    meta.dataset._children = originalDatasets;

    points.forEach(function (point) {
      point.draw(area);
    });
  },
});

const CustomLine = generateChart("custom-line", "multicolorLine");

export default {
  name: "HelloWorld",
  extends: CustomLine,
  mounted() {
    this.renderChart(this.chartdata, this.options);
  },
  data() {
    return {
      chartdata: {
        labels: [
          "a",
          "b",
          "c",
          "d",
          "e",
          "f",
          "g",
          "h",
          "i",
          "j",
          "k",
          "l",
          "m",
          "n",
        ],
        datasets: [
          {
            label: "My First dataset",
            borderColor: "rgb(255, 99, 132)",
            data: [0, 10, 15, 20, 25, 30, 27, NaN, 15, 12, 19, 28, 37, 46],
            //first color is not important
            // colors: [
            //   0,
            //   10,
            //   15,
            //   20,
            //   25,
            //   30,
            //   27,
            //   NaN,
            //   15,
            //   12,
            //   19,
            //   28,
            //   37,
            //   46,
            // ]
            colors: [
              0,
              10,
              15,
              20,
              25,
              30,
              27,
              NaN,
              15,
              12,
              19,
              28,
              37,
              46,
            ].map((dat) => {
              if (dat < 20) {
                return "red";
              }
              if (isNaN(dat)) {
                console.log("isNaN");
                return "#d5e6f7";
              } else return "#62de6a";
              // (dat < 20 ? "lime" : "red")
            }),
          },
        ],
      },
      options: {},
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
