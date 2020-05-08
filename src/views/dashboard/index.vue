<template>
  <div class="dashboard-container">
    <div class="dashboard-text">44</div>
    <people-manage />
  </div>
</template>

<script>
import peopleManage from './peopleManage'

export default {
  name: 'Dashboard',
  components: {
    peopleManage
  },
  data() {
    return {}
  },
  created() {
  },
  methods: {}
}
</script>

<style lang="scss" scoped>
  .dashboard {
    &-container {
      margin: 30px;
    }

    &-text {
      font-size: 30px;
      line-height: 46px;
    }
  }
</style>
