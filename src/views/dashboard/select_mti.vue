<template>
  <div class="container">
    <div class="editbox" @click="toggle">
      <i class="el-icon-edit edit"/>
    </div>

    <div v-show="showPannel" class="selectoptionBox">
      <div class="search_icon">
        <svg-icon icon-class="search"/>
      </div>

      <div class="input">

        <input v-model.lazy.trim="keyword" :placeholder="palaceholder" @input="search($event)">
      </div>
      <div v-if="list.length>0" v-infinite-scroll="load" class="scrolling menu">
        <div
          :key="item.id"
          v-for="item in list"
          class="item"
          :class="{'active':current&&item.id === current.id}"
          data-value="0"
          @click="selectItem(item)"
        >{{ item.name }}
        </div>
      </div>
      <div v-else class="message ">未找到合适的结果</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SelectMti',
  props: {
    current: {
      type: Object,
      default: null
    },
    list: {
      type: Array,
      default: null
    },
    palaceholder:{
      type:String,
      default: '输入搜索...'
    }
  },
  data() {
    return {
      selected: {id: 3, name: '无里程碑'},
      showPannel: false,
      selectedItem: null,
      keyword: '',
    }
  },
  methods: {
    load() {
      this.$emit('load')
    },
    toggle() {
      this.showPannel = !this.showPannel
    },
    selectItem(item) {
      // this.selectedItem = item
      this.$emit('selectItem', item)
      this.showPannel = false
    },
    search(e) {
      console.log(e.target)


      this.$emit('search', e.target.value)
    }
  }
}
</script>

<style lang="less" scoped>
  .container {
    position: absolute;

    .editbox {
      padding: 2px;
      cursor: pointer;

      .edit {
        color: #4a90e2;

      }
    }

    .selectoptionBox {
      display: inline-block;
      top: 26px;
      left: 0;
      position: absolute;
      min-width: 220px;
      max-width: 400px;
      min-height: 142px;
      border: 0;
      border-radius: 0;
      background: #FFF;

      box-shadow: 0px 2px 4px 0px rgba(34, 36, 38, 0.12), 0px 2px 10px 0px rgba(34, 36, 38, 0.15) !important;

      .search_icon {
        position: absolute;
        /*margin: 1.14285714rem 0.78571429rem;*/
        height: 34px;
        margin-left: 1.5em;
        margin-top: 1.1em;
        display: flex;
        color: rgba(0, 0, 0, 0.8);
        align-items: center;

      }

      .input {
        display: flex;
        margin: 1em;

        input {
          height: 34px;
          padding-left: 2em;
          box-shadow: none;
          width: 100%;
          border-radius: 3px;
          border: 1px solid #dfe3e9;

          &:focus {
            border-color: rgba(254, 115, 0, 0.5);
            outline: none;
          }
        }
      }

      .message {
        color: rgba(0, 0, 0, 0.4);
        line-height: 1.333;
        padding: 0.78571429rem 1.14285714rem !important;

        padding-top: 0.7142857rem !important;
        padding-bottom: 0.7142857rem !important;
      }

      .menu {
        max-height: 170px;
        overflow-y: auto;

        .item {
          text-overflow:ellipsis;
          overflow:hidden;
          white-space: nowrap;
          line-height: 1.333;
          padding-top: 0.7142857rem !important;
          padding-bottom: 0.7142857rem !important;
          position: relative;
          cursor: pointer;
          display: block;
          height: auto;
          text-align: left;
          border-top: none;
          line-height: 1em;
          color: rgba(0, 0, 0, 0.87);
          padding: 0.78571429rem 1.14285714rem !important;
          font-size: 1rem;
          text-transform: none;
          font-weight: normal;

          &.active {
            background: rgba(200, 200, 200, .6);
          }

          &:hover {
            background: rgba(200, 200, 200, .6);
          }
        }
      }
    }

  }

</style>
