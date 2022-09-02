<template>
  <DataInsert />
  <DataList />
  <MachineInfo />
</template>

<script>
import DataInsert from './components/DataInsert.vue'
import DataList from './components/DataList.vue'
import MachineInfo from './components/MachineInfo.vue'
/* import axios from 'axios' */

export default {
  name: 'App',
  components: {
    DataInsert,
    DataList,
    MachineInfo
  },
  data () {
    return {
      title: 'My First Vue App'
    }
  },
}
</script>

<style>
.app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
h1 {
  border-bottom: 1px solid #ddd;
  display: inline-block;
  padding-bottom: 10px;
}
</style>
