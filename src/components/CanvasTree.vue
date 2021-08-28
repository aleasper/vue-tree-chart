<template>
  <div id="org-chart-container">
    <div class="menu-container">
      <person
        v-if="personIsSelected"
        :person="selectedPerson"
      ></person>
    </div>
  </div>
</template>

<script lang="ts">
import OrgChart from './org-chart'
import Vue from 'vue'
import { generateOrgChartData, Data } from '../base/data-generator'
import { getRequest } from '../base/http-work'
import Person from './Person.vue';

export default Vue.extend({
  name: 'org-chart',
  components: {
    'person': Person
  },
  data() {
    return {
      data: null,
      orgChart: null,
      supportActions: [
        'click node to toggle',
        'drag canvas',
        'use mouse wheel to zoom',
        'button control to zoom'
      ],
      selectedPerson : {},
      personIsSelected: false,

      backendURL: 'http://172.24.8.169:5000'
    }
  },
  created() {
    // this.data = generateOrgChartData(10);
  },
  mounted() {
    getRequest(`${this.backendURL}/api/structure`, '', {}).then((res) => {
      if (!res['status'] || !res['body']['status']) {
        alert('Всё плохо)')
        return
      }
      console.log(res)
      this.tree = res['body']['tree']
      this.data = this.tree[0]
      console.log(this.data);

      this.orgChart = new OrgChart(this);
      this.orgChart.draw(this.data);
    })
  },
  methods: {
    test() {
      this.orgChart.draw(this.data)
    },
    bigger() {
      this.orgChart.bigger()
    },
    smaller() {
      this.orgChart.smaller()
    },
    updateData(data) {
      this.data = data
      this.orgChart.draw(this.data)
    },
    selectPerson(person) {
      this.selectedPerson = person;
      this.personIsSelected = Object.keys(this.selectedPerson).length !== 0;
    }
  }
})
</script>

<style scoped>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.orgChart {
  border: 1px solid black;
  height: 100%;
}

.menu-container {
  position: absolute;
  display: flex;
  align-items: center;
  flex-direction: column;
  vertical-align: top;
  width: 30vw;
  min-width: 300px;
  height: 100%;
  background-color: #f5f5f5;
  border-right: 2px solid #2196f3;
  padding: 0.4em;
}
.action-title {
  font-size: 28px;
}

.action-item {
  font-size: 24px;
}
</style>
