<template>
  <div class="container">
    <div class="selectedPersons" @click="toggle">
      <div class="personsIncharge">
        <span class="title" v-if="personsIncharge.length>0">负责人:</span>
        <div class="peopleInfo" v-for="item in personsIncharge">
          <img
            class="avator"
            :src="item.avator"
          ><span
            class="name"
          >{{item.name}}</span>
        </div>
      </div>
      <span class="title" v-if="collaborators.length>0">协作者:</span>

      <div class="Collaborator">
        <div class="peopleInfo" :key="item.name" v-for="(item,index) in collaborators"  v-if="index<3">
          <img

            class="avator"
            :src="item.avator"          >
          <span
            v-if="collaborators.length<2"
            class="name"
        >{{item.name}}</span>
        </div>
      </div>
      <span class="extra" v-if="collaborators.length>3">+{{collaborators.length -3}}</span>
    </div>
    <div v-show="showPannel" class="allPeoples">
      <div class="searchBox">
        <i class="el-icon-search" />
        <input class="search" placeholder="搜索用户...">

      </div>
      <div class="countsHeader">
        <span>项目成员(1/9)</span>
      </div>
      <div v-for="(item,index) in persons" class="people" :class="{ isPersonIncharge: item.isPersonIncharge, 'isCollaborator': item.isCollaborator }">
        <div class="peopleInfo">
          <img
            class="avator"
            :src="item.avator"
          ><span
            class="name"
          >{{ item.name }}</span>
        </div>
        <div class="right">

          <div v-if="item.isPersonIncharge || item.isCollaborator" class="del">
            <span v-if="item.isPersonIncharge" class="tag1">负责人</span>
            <span v-if="item.isCollaborator" class="tag2">协作者</span>
            <span class="tag" @click="unSet(index)"><i class="el-icon-close" /></span>
          </div>
          <div v-else class="add">
            <span class="tag" @click="setPersonIncharge(index)">+负责人</span>
            <span class="tag" @click="setCollaborator(index)">+协作者</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PeopleManage',
  data() {
    return {
      selected: {
        personIncharge: {

        }
      },
      persons: [{
        name: 'zhangsanfeng',
        avator: 'https://portrait.gitee.com/uploads/avatars/user/477/1432225_moce-technology_demoosc_1578951338.png!avatar30',
        isPersonIncharge: true,
        isCollaborator: false
      }, {
        name: 'lichade',
        avator: 'https://portrait.gitee.com/uploads/avatars/user/477/1432225_moce-technology_demoosc_1578951338.png!avatar30',
        isPersonIncharge: false,
        isCollaborator: true
      }, {
        name: 'shanghai',
        avator: 'https://portrait.gitee.com/uploads/avatars/user/477/1432225_moce-technology_demoosc_1578951338.png!avatar30',
        isPersonIncharge: false,
        isCollaborator: false
      }, {
        name: 'heiil',
        avator: 'https://portrait.gitee.com/uploads/avatars/user/477/1432225_moce-technology_demoosc_1578951338.png!avatar30',
        isPersonIncharge: false,
        isCollaborator: false
      }],
      showPannel: false
    }
  },
  computed: {
    personsIncharge: function () {
      return this.persons.filter(item =>{
        return item.isPersonIncharge === true
      })
    },
    collaborators: function () {
      return this.persons.filter(item =>{
        return item.isCollaborator === true
      })
    }
  },
  methods: {
    toggle() {
      this.showPannel = !this.showPannel
    },
    setPersonIncharge(index) {
      this.persons.forEach(item => {
        item.isPersonIncharge = false
      })
      this.persons[index].isPersonIncharge = true
    },
    setCollaborator(index) {
      this.persons[index].isCollaborator = true
    },
    unSet(index) {
      this.persons[index].isPersonIncharge = false
      this.persons[index].isCollaborator = false
    }
  }
}
</script>

<style lang="less" scoped>
  .container{
    position: relative;
    .avator {
      width: 22px;
      height: 22px;
      border-radius: 50%;
      margin-right: 2px;
    }
  }
  .selectedPersons {
    width: 330px;


    height: 32px;
    border: 1px solid #97a8be;
    border-radius: 4px;
    display: flex;
    align-items: center;
    padding: 3px 10px;
    /*overflow: hidden;*/

    .title {
      color: #ccc;
      font-size: .8em;
      margin-right: 9px;
      flex-shrink:0
    }
    .peopleInfo {
      display: flex;
      align-items: center;
      padding: 2px 4px;
      background: #f2f2f2;
      /*display: inline-block;*/
      border-radius: 3px;
      pointer-events: none;
     height: 26px;
      margin-right: 6px;

      .name {
        color: #97a8be;
        font-size: .8em;
        line-height: 32px;
      }

    }
    .extra{
      font-size: 12px;
      color: gray;
    }

    .personsIncharge ,.Collaborator{
      display: flex;
      align-items: center;
      margin-right: 8px;
      flex-shrink:0

    }

  }
  .allPeoples{
    width: 326px;
    height: 300px;
    overflow: scroll;
    background: white;
    position: absolute;
    top: 40px;
    box-shadow:0px -2px 2px 0px #eee,   /*上边阴影  红色*/
    -2px 0px 2px 0px #eee,   /*左边阴影  绿色*/
    2px 0px 2px 0px #eee,    /*右边阴影  蓝色*/
    0px 2px 0px 0px #eee;
    .searchBox{
      margin:12px 16px 6px 16px;
      i{
        position: absolute;
        right: 2em;
        margin-top: 5px;
        /*top: 3px;*/
      }
      .search{
        width: 100%;
        font-size: 12px;
        padding: 0.5em 1em;
        border-radius: 3px;
        border: 1px solid #dfe3e9;
      }
    }
    .countsHeader{
      background: #F0F0F0;
      line-height: 34px;
      height: auto;
      padding-left: 16px;
      color: #40485b;
      cursor: pointer;
      border-bottom: 1px solid #ebeef5;
      font-size: 13px;
      font-weight: 500;
    }

    .people{
      padding: 4px 15px;
      display: flex;
      justify-content: space-between;
      &.isPersonIncharge{
        background: rgba(96,183,0,0.1);
      }
      &.isCollaborator{
        background: rgba(74,144,226,0.1);
      }
      .peopleInfo{
        display: flex;
        align-items: center;
        padding: 2px 4px;
        border-radius: 3px;
        pointer-events: none;
        height: 26px;
        margin-right: 6px;

        .name {
          color: #97a8be;
          font-size: .8em;
          line-height: 32px;
        }
      }
      .right{
        display: flex;
        align-items: center;
        .add{
          .tag{
            color: #005980;
            font-size: 12px;
            line-height: 18px;
            padding: 2px 6px;
            background: #F5F6F8;
            border-radius: 2px;
            display: inline-block;
            margin: 0 0 0 5px;
            cursor: pointer;
            /*margin: 3px;*/
          }

        }
        .del{
          color: #4a90e2;
          font-size: .8em;
          display: flex;
          align-items: center;
          .tag2{
            color: #60b700;
          }
          span:first-child{
            margin-right: 3px;
          }
          span:last-child{
            display: inline-block;
            color: #d0021b;
            background: rgba(208,2,27,0.1);
            font-size: 1.4em;
            padding: 1px 4px;

          }
        }
      }

    }
  }
</style>
