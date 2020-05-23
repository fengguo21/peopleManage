<template>
  <div class="dashboard-container">
    <div class="dashboard-text">44</div>
    <people-manage :selected-persons="selectedPersons"/>
<span>{{selectedItem?selectedItem.name:''}}</span>
    <select_mti @selectItem="selectItem($event)"></select_mti>
  </div>
</template>

<script>
import peopleManage from './peopleManage'
import select_mti from './select_mti'

export default {
  name: 'Dashboard',
  components: {
    peopleManage,
    select_mti
  },
  data() {
    return {
      selectedItem:'',
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
    selectItem(item){
      this.selectedItem = item
    }
  }
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
