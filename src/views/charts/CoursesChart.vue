<template>
  <CChartDoughnut :data="defaultData" />
</template>

<script>
import { CChartDoughnut } from '@coreui/vue-chartjs'
export default {
  name: 'CoursesChart',
  components: { CChartDoughnut },
  computed: {
    defaultData() {
      return {
        labels: ['Matemática', 'Letras', 'Geografia'],
        datasets: [
          {
            backgroundColor: ['#41B883', '#E46651', '#00D8FF'],
            data: [40, 20, 80],
          },
        ],
      }
    },
  },
}
</script>
