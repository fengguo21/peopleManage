<template>
  <div class="dashboard-container">
    <!--    <div class="content">-->
    <!--      <div class="dashboard-text">44</div>-->
    <!--      <people-manage :selected-persons="selectedPersons"/>-->
    <!--      <span>{{selectedItem?selectedItem.name:''}}</span>-->

    <!--    </div>-->
    <div>
      <!--      <side_bar></side_bar>-->
    </div>
<!--    <table_mti @showDetail="showDetail($event)" :list="mylist"/>-->
    <mti_button medium @click="clickButton">创建</mti_button>
    <mti_button medium><i class="el-icon-plus"/> 新建任务</mti_button>
    <mti_button basic>新建任务</mti_button>
    <select_mti :list="list" @load="loadmore" :current="selectedItem" @search="search($event)" palaceholder="搜索里程碑..."
                @selectItem="selectItem($event)"></select_mti>
  </div>

</template>

<script>
import peopleManage from './peopleManage'
import select_mti from './select_mti'
import table_mti from './table_mti'
import side_bar from './side_bar'

export default {
  name: 'Dashboard',
  components: {
    peopleManage,
    select_mti,
    side_bar,
    table_mti,
  },
  data() {
    return {
      mylist: [
        {
          name: 'zhang', age: 15, job: 'teacher', id: 1,
          children: [{name: 'zhang', age: 15, id: 2, job: 'teacher'},
            {
              name: 'zhang', age: 15, id: 3, job: 'teacher', children: [{id: 4, name: 'zhang', age: 15, job: 'teacher'},
                {id: 5, name: 'zhang', age: 15, job: 'teacher'},]
            }]
        },
        {id: 6, name: 'zhang', age: 15, job: 'teacher'},
        {id: 7, name: 'zhang', age: 15, job: 'teacher'},
        {id: 8, name: 'zhang', age: 15, job: 'teacher'},
        {id: 9, name: 'zhang', age: 15, job: 'teacher'},
        {id: 10, name: 'zhang', age: 15, job: 'teacher'},
        {id: 11, name: 'zhang', age: 15, job: 'teacher'}
      ],
      list: [
        {id: 1, name: '无里程sadfgdsf sdfg dg sdfgsfsgfsdfa是的风格是的风格是的风格是的风格碑'},
        {id: 2, name: '无里程碑'},
        {id: 3, name: '无里程碑'},
        {id: 4, name: '无里程碑'},
        {id: 5, name: '无里程碑'},
        {id: 6, name: '无里程碑'},
        {id: 7, name: '无里程碑'},
        {id: 8, name: '无里程碑'},
        {id: 9, name: '无里程碑'}
      ],
      selectedItem: {},
      selectedPersons: [
        {
          name: 'zhangsanfeng',
          avator: 'https://portrait.gitee.com/uploads/avatars/user/477/1432225_moce-technology_demoosc_1578951338.png!avatar30',
          isManager: true,
          id: 1,
          isCollaborator: false
        },
        {
          name: 'lichade',
          avator: 'https://portrait.gitee.com/uploads/avatars/user/477/1432225_moce-technology_demoosc_1578951338.png!avatar30',
          isManager: false,
          id: 1,
          endTime: '20200909 00:00:00',
          hours: 12,
          isCollaborator: false
        }
      ]
    }
  },
  computed: {
    selectedPeopleManage: function () {
      return this.selectedPersons.filter(item => {
        return item.isManager === true
      })
    },
    selectedColaboter: function () {
      return this.selectedPersons.filter(item => {
        return item.isManager === false
      })
    }
  },
  created() {
  },
  methods: {
    clickButton() {
      console.log(';clickbutton')
    },
    showDetail(item) {
      console.log(item.id, 'parteng=======')
    },
    search(e) {
      console.log('search', e)
    },
    selectItem(item) {
      this.selectedItem = item
    },
    loadmore() {
      console.log('more---')
    }
  }
}
</script>

<style lang="scss" scoped>
  /*.dashboard-container {*/
  /*  display: flex;*/
  /*  min-height: calc(100vh - 50px);*/

  /*  .content {*/
  /*    height: 100%;*/
  /*    flex: 1;*/
  /*    min-height: 100%;*/
  /*  }*/
  /*}*/

  /*.dashboard-text {*/
  /*  font-size: 30px;*/
  /*  line-height: 46px;*/
  /*}*/
</style>
