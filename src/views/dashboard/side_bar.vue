<template>
  <div class="container">
    <div class="ent-resource-sidebar-toggle" @click="toggle">
      <svg-icon class="toggle" :class="{'isopen':showMenu}"  icon-class="toggle"/>
    </div>
    <transition name="toggle">
      <div v-show="showMenu" class="ent-issues-sidebar">
        <div class="ui header">
          任务完成率统计
        </div>
        <div ref="chart" :style="{height:'180px',width:'213px'}"/>
        <div class="menu">
          <h3>全部任务</h3>
          <h3>快捷筛选</h3>
          <h4>
            当天任务
          </h4>
          <h4>
            本周任务
          </h4>
          <h4>
            本月任务
          </h4>

          <h3>我的任务</h3>
          <h4>
            指派给我的
          </h4>
          <h4>
            我发布的
          </h4>
          <h4>
            我参与的
          </h4>
        </div>
      </div>

    </transition>

  </div>

</template>

<script>
import echarts from 'echarts'

export default {

  name: 'SideBar',
  data(){
    return{
      showMenu:true,
    }
  },
  methods:{
    toggle(){
      this.showMenu = ! this.showMenu
    }
  },
  mounted() {
    const option = {
      tooltip: {
        trigger: 'item',
        formatter: '{b}: {c}个'
      },
      title: {
        text: '40%',
        left: 'center',
        top: 'center',
        textStyle: {
          color: '#000',
          fontSize: 36,
          fontWeight: 400
        }
      },
      color: ['#febc0a', '#fe7300', '#4a90e2', '#eb031a'],

      series: [
        {
          name: '访问来源',
          type: 'pie',
          radius: ['55%', '80%'],
          avoidLabelOverlap: false,
          label: {
            show: false,
            position: 'center'
          },
          labelLine: {
            show: false
          },
          data: [
            {value: 335, name: '已完成'},
            {value: 310, name: '已拒绝'},
            {value: 234, name: '进行中'},
            {value: 135, name: '未开始'}
          ]
        }
      ]
    }

    console.log(echarts, '--- d')
    const chart = echarts.init(this.$refs.chart)
    chart.setOption(option)
  }
}
</script>

<style lang="less" scoped>
  .toggle-enter-active {
    animation: toggle .3s ease;
  }
  .toggle-leave-active {
    animation: toggle .3s ease reverse;
  }
  @keyframes toggle {
    0% {
      margin-right: -246px;
    }
    100% {
      margin-right: 0px;

    }
  }
  .container {
    display: flex;
    height: 100%;
  }

  .ent-resource-sidebar-toggle {
    z-index: 1;
    height: 100%;
    background: #eff4f7;
    -webkit-box-align: center;
    -ms-flex-align: center;
    align-items: center;
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    font-size: 30px;
    font-weight: bold;
    width: 10px;
    text-align: center;
    border-left: 1px solid #e4eaed;
    border-left-width: 1px;
    border-left-style: solid;
    border-left-color: rgb(228, 234, 237);
    .toggle{
      color: #8c92a4;
      &.isopen{
        transform: rotate(180deg);
      }
    }
  }

  .ent-issues-sidebar {


    width: 246px;
    height: 100%;
    -webkit-box-flex: 0;
    -webkit-flex-grow: 0;
    -moz-box-flex: 0;
    -ms-flex-positive: 0;
    flex-grow: 0;
    -webkit-flex-shrink: 0;
    -ms-flex-negative: 0;
    flex-shrink: 0;
    padding: 15px 16px;
    border-left: 1px solid #dce3e8;
    background: #f7f7f7;

    .ui.header {
      font-size: 1rem;
      line-height: 20px;
      margin-bottom: 15px;
      font-weight: bold;
    }

    .ui.header:first-child {
      margin-top: -0.165em;
    }

    .menu {
      h3 {
        font-size: 1em;
        line-height: 20px;
        font-weight: bold;
        color: #40485b;
        cursor: pointer;

        &:nth-child(1):hover, &:nth-child(6):hover {
          color: #4a90e2;
        }

        &:nth-child(2) {
          cursor: default;
        }
      }

      h4 {
        color: #005980;
        padding: 0px 0 0px 12px;
        display: list-item;
        table-layout: fixed;
        list-style-type: none;
        list-style-position: outside;
        line-height: 1.2;
        font-weight: 400;
        font-size: 1em;
        cursor: pointer;

        &:hover {
          color: #4a90e2;
        }
      }
    }
  }
</style>
