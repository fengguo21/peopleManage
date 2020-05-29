<template>
  <div>
    <div class="table">
      <template v-for="(item,index) in list">
        <div class="tr" :key="'p'+index">
          <span class="hasChild" v-if="item.children" @click="expand(index)"></span>
          <span>{{index}}</span>
          <span @click="clickitem(item)">{{item.name}}</span>
          <span>{{item.age}}</span>
          <span>{{item.job}}</span>
        </div>
        <div :key="index" v-if=" item['isexpand'] === true">
          <table-mti :list="item.children"/>
        </div>

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
      default: function () {
        return []
      }
    }
  },
  data() {
    return {
      isexpand: false
    }
  },
  methods: {
    expand(index) {
      console.log(index, 'index')
      console.log(false === false)
      this.$set(this.list[index], 'isexpand', this.list[index]['isexpand'] !== true)

      console.log(this.list[index])
    },
    clickitem(item) {
      console.log(item.id)
      this.$emit('showDetail', item)
    },

  }
}
</script>

<style lang="less" scoped>
  * {
    margin: 0;
    padding: 0;
  }

  .table {
    color: black;
    margin-left: 20px;
    /*border: 1px solid black;*/

    .tr {
      display: flex;
      justify-content: flex-start;
      border-bottom: 1px gray solid;
      /*margin-left: 6px;*/
      position: relative;

      align-items: center;

      &:hover {
        background: red;
      }

      span {
        text-align: left;
        width: 100px;

        &.hasChild {
          width: 0px;
        }
      }

      span.hasChild:before {
        content: '';
        display: block;
        width: 20px;
        height: 10px;
        /*background: black;*/
        margin-left: -20px;

        border: 10px solid transparent;
        border-top: 10px solid #AFABAB;
        position: relative;
        top: 2px;

      }
    }
  }
</style>
