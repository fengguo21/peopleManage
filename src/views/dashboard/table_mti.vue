<template>
  <div>
    <div class="table">
      <template v-for="(item,index) in list">
        <div class="tr" :key="index" @click="expand = !expand">
          <span>{{index}}</span>
          <span>{{item.name}}</span>
          <span>{{item.age}}</span>
          <span>{{item.job}}</span>
        </div>
        <table-mti v-if="item.children && expand" :list="item.children"/>
      </template>

    </div>
  </div>
</template>

<script>
export default {
  name: 'TableMti',
  props: {
    list: {
      type: Array,
      default: []
    }
  },
  data() {
    return {
      expand:false
    }

  }
}
</script>

<style lang="less" scoped>
  .table {
    color: red;
    margin-left: 5px;
    border: 1px solid black;

    .tr {

      margin-left: 6px;


    }
  }
</style>
