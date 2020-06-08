<template>
  <div class="dashboard-container">
    <vue-wangeditor ref="editor"  uploadImgUrl="http://www.wangeditor.com/" :menus="menus" id="editor" v-model="text" :isRealtime="true" @change="changeCotent"/>
  </div>

</template>

<script>
import { Subject } from 'rxjs'
import { debounceTime, distinctUntilChanged } from 'rxjs/operators'
import peopleManage from './peopleManage'
import select_mti from './select_mti'
import table_mti from './table_mti'
import side_bar from './side_bar'
const subject =  new Subject()
import vueWangeditor from 'vue-wangeditor'
export default {
  name: 'Dashboard',
  components: {
    peopleManage,
    select_mti,
    side_bar,
    table_mti,
    vueWangeditor
  },
  data() {
    return {
      hideLinkImg:'true',
      menus:[
        'source',	// 源码模式
        '|',
        'bold',	// 粗体
        'underline',	// 下划线
        'italic',	// 斜体
        'strikethrough',	// 中线
        'eraser',	// 清空格式
        'forecolor',	// 文字颜色
        'bgcolor',	// 背景颜色
        '|',
        'quote',	// 引用
        'fontfamily',	// 字体
        'fontsize',	// 字号
        'head',	// 标题
        'unorderlist',	// 无序列表
        'orderlist',	// 有序列表
        'alignleft',	// 左对齐
        'aligncenter',	// 居中
        'alignright',	// 右对齐
        '|',
        'link',	// 链接
        'unlink',	// 取消链接
        'table',	// 表格
        'emotion',	// 表情
        '|',
        'img',	// 图片
        // 'video',	// 视频
        // 'location',	// 位置
        // 'insertcode',	// 插入代码
        '|',
        'undo',	// 撤销
        'redo',	// 重做
        'fullscreen'	// 全屏
      ],
      text:'',
      // input content to editor
      content: 'base on wangeditor',
      // output content from editor
      result: '',
      // set image upload api url
      path: '/api/v1/help/upload/wangEditorH5File',

      mylist: [
        {
          name: 'zhang', age: 15, job: 'teacher', id: 1,
          children: [{ name: 'zhang', age: 15, id: 2, job: 'teacher' },
            {
              name: 'zhang', age: 15, id: 3, job: 'teacher', children: [{ id: 4, name: 'zhang', age: 15, job: 'teacher' },
                { id: 5, name: 'zhang', age: 15, job: 'teacher' }]
            }]
        },
        { id: 6, name: 'zhang', age: 15, job: 'teacher' },
        { id: 7, name: 'zhang', age: 15, job: 'teacher' },
        { id: 8, name: 'zhang', age: 15, job: 'teacher' },
        { id: 9, name: 'zhang', age: 15, job: 'teacher' },
        { id: 10, name: 'zhang', age: 15, job: 'teacher' },
        { id: 11, name: 'zhang', age: 15, job: 'teacher' }
      ],
      list: [
        { id: 1, name: '无里程sadfgdsf sdfg dg sdfgsfsgfsdfa是的风格是的风格是的风格是的风格碑' },
        { id: 2, name: '无里程碑' },
        { id: 3, name: '无里程碑' },
        { id: 4, name: '无里程碑' },
        { id: 5, name: '无里程碑' },
        { id: 6, name: '无里程碑' },
        { id: 7, name: '无里程碑' },
        { id: 8, name: '无里程碑' },
        { id: 9, name: '无里程碑' }
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
    selectedPeopleManage: function() {
      return this.selectedPersons.filter(item => {
        return item.isManager === true
      })
    },
    selectedColaboter: function() {
      return this.selectedPersons.filter(item => {
        return item.isManager === false
      })
    }
  },
  created() {
    subject.pipe(
      debounceTime(500),
      distinctUntilChanged()
    ).subscribe({
      next: (v) => console.log(`observerA: ${v}`)
    })
  },
  methods: {
    changeCotent(){

      console.log(this.$refs.editor.getHtml(),'--------')
    },
    searchData(val) {
      console.log(val,)
      subject.next(val.target.value)
    },
    clickButton() {
      console.log(';clickbutton')
    },
    showDetail(item) {
      console.log(item.id, 'parteng=======')
    },
    search(e) {
      subject.next(e)
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
