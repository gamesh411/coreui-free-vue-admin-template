<script>
import { Line } from 'vue-chartjs'
import { CustomTooltips } from '@coreui/coreui-plugin-chartjs-custom-tooltips'
import { hexToRgba } from '@coreui/coreui/dist/js/coreui-utilities'

export default {
  components: {
    hexToRgba,
    CustomTooltips
  },
  extends: Line,
  watch: {
    '$route' (to, from) {
      this.onMounted()
    }
  },
  methods: {
    randomData: () => Array.from({length: 7}, () => Math.floor(Math.random() * 100)),
    onMounted () {
      this.renderChart(
      {
        labels: ['January', 'February', 'March', 'April', 'May', 'June', 'July'],
        datasets: [
          {
            label: 'Data One',
            backgroundColor: hexToRgba('#E46651', 90),
            data: this.randomData()
          },
          {
            label: 'Data Two',
            backgroundColor: hexToRgba('#00D8FF', 90),
            data: this.randomData()
          }
        ]
      },
      {
        responsive: true,
        maintainAspectRatio: true,
        tooltips: {
          enabled: false,
          custom: CustomTooltips,
          intersect: true,
          mode: 'index',
          position: 'nearest',
          callbacks: {
            labelColor: function (tooltipItem, chart) {
              return { backgroundColor: chart.data.datasets[tooltipItem.datasetIndex].backgroundColor }
            }
          }
        }
      }
    )
    }
  },
  mounted () { this.onMounted() }
}
</script>
