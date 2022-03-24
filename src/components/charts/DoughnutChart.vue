<script>
import { Doughnut, mixins } from 'vue-chartjs'

export default {
  extends: Doughnut,
  mixins: [mixins.reactiveProp],
  props: {
    chartData: {
      type: Object,
      required: true
    }
  },
  data () {
    return {
      gradient: null
    }
  },
  methods: {
    update() {
      this.$data._chart.update()
    },
  },
  mounted () {
    this.gradient = this.$refs.canvas.getContext('2d').createLinearGradient(100, 100, 0, 200)

    this.gradient.addColorStop(0, '#B0D4E2')
    this.gradient.addColorStop(0.5, '#61B058')
    this.gradient.addColorStop(1, '#61B058')

    this.addPlugin({
      id: 'main-plugin',
      beforeDraw: (chart) => {
        let width = chart.chart.width;
        let height = chart.chart.height;
        let ctx = chart.chart.ctx;

        ctx.restore();
        let fontSize = (height / 114).toFixed(2);
        ctx.font = fontSize + 'em Open Sans';
        ctx.textBaseline = 'middle';

        let finishedCount = chart.data.datasets[0].data[0];
        let ongoingCount = chart.data.datasets[0].data[1];

        let text = Math.round(finishedCount / (finishedCount + ongoingCount) * 100) + '%';

        let textX = Math.round((width - ctx.measureText(text).width) / 2);
        let textY = height / 2;

        ctx.fillText(text, textX, textY);
        ctx.save();
      },
    })

    this.renderChart({
      datasets: [
          {
            borderWidth: 0,
            backgroundColor: [this.gradient, '#F1F2F3'],
            data: this.chartData.datasets[0].data
          }
        ]
      }, 
      {
        responsive: true, 
        maintainAspectRatio: false, 
        animation: { animateRotate: false },
        legend: { display: false },
        tooltips: { enabled: false },
        cutoutPercentage: 80
      }
    )
  }
};
</script>
