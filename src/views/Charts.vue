<template>
  <div class="animated fadeIn">
    <b-card-group columns class="card-columns">
      <template v-if="!services">
        <b-card header="Info">
          <p>This environment does not have any services</p>
        </b-card>
      </template>
      <template v-else>
        <b-card v-for="service in services" :header="service.name">
          <div class="chart-wrapper">
            <line-example chartId="chart-line-01"/>
          </div>
        </b-card>
      </template>
    </b-card-group>
  </div>
</template>
<script>
import sampledata from '@/sampledata'

import BarExample from './charts/BarExample'
import LineExample from './charts/LineExample'
import DoughnutExample from './charts/DoughnutExample'
import RadarExample from './charts/RadarExample'
import PieExample from './charts/PieExample'
import PolarAreaExample from './charts/PolarAreaExample'

export default {
  name: 'charts',
  components: {
    BarExample,
    LineExample,
    DoughnutExample,
    RadarExample,
    PieExample,
    PolarAreaExample
  },
  computed: {
    routeId () { return this.$route.params.id },
    services () {
      const environment = sampledata.environments.find(env => env.id === this.routeId)
      return environment ? environment.services : null
    }
  }
}
</script>
