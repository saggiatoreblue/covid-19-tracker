<script>
import { Pie } from 'vue-chartjs';

export default {
  extends: Pie,

  props: {
    chartData: {
      type: Object
    }
  },

  mounted() {

    const cases = this.chartData.cases;
    const deaths = this.chartData.deaths;
    const vaccinations = this.chartData.vaccinations;

    const options = {
      responsive: true,
      maintainAspectRatio: false
    }

    const data = {
      labels: [
        'Cases',
        'Deaths',
        'Vaccinations'
      ],
      datasets: [{
        label: 'COVID DATA',
        data: [cases, deaths, vaccinations],
        backgroundColor: [
          'rgb(42,109,5)',
          'rgb(133,18,18)',
          'rgb(33,67,119)'
        ],
        hoverOffset: 4
      }]
    };
    this.renderChart(data, options);

  }

}
</script>


