<template>

  <div>
    <h2>输出值：{{ result }}</h2>
    <input v-model="result">{{ result }}
    <button @click="goback">返回</button>
    <button @click="changeData">改变</button>
    <h3>{{ message }}</h3>
    <p>Original message: "{{ message }}"</p>
    <p>Computed reversed message: "{{ reversedMessage }}"</p>
    <h2>随便写点啥，zzzzz</h2>
    <ul>
      <li v-for="(item,index) in items" :key="item.message">
        {{ index }}+++++{{ item.message }}
      </li>
    </ul>
    单位：
    <select v-model="UnitSelected">
      <option v-for="item in UnitList" :value="item.id" :key="item.id">{{ item.name }}</option>
    </select>
    部门：
    <select v-model="DepartmentSelected">
      <option v-for="item in DepartmentList" :value="item.id" :key="item.id">{{ item.name }}</option>
    </select>
    用户：
    <select v-model="UserSelected">
      <option v-for="item in UserList" :value="item.id" :key="item.id">{{ item.name }}</option>
    </select>

  </div>

</template>

<script>
var UnitRows = [
  {name: '1', id: '1'},
  {name: '2', id: '2'}
]
var DepartmentRows = [
  {name: '11', id: '1', pid: '1'},
  {name: '12', id: '2', pid: '1'},
  {name: '21', id: '3', pid: '2'},
  {name: '22', id: '4', pid: '2'}
]
var UserRows = [
  {name: '111', id: '1', pid: '1'},
  {name: '112', id: '2', pid: '1'},
  {name: '121', id: '3', pid: '2'},
  {name: '122', id: '4', pid: '2'},
  {name: '211', id: '5', pid: '3'},
  {name: '212', id: '6', pid: '3'},
  {name: '221', id: '7', pid: '4'},
  {name: '222', id: '8', pid: '4'}
]
export default {
  // el: '#app-2',
  name: 'FirstVue',
  data () {
    return {
      result: '我是一颗小虎牙',
      message: 'test',
      count: 0,
      items: [
        {message: 'Foo'},
        {message: 'Bar'}
      ],
      object: {
        title: 'How to do lists in Vue',
        author: 'Jane Doe',
        publishedAt: '2016-04-10'
      },
      UnitSelected: '',
      UnitList: [],
      DepartmentSelected: '',
      DepartmentList: [],
      UserSelected: '',
      UserList: []

    }
  },
  methods: {
    goback () {
      this.$router.back()
    },
    changeData () {
      this.result = '被改变了' + this.count++
    }
  },
  computed: {
    // 计算属性的 getter
    reversedMessage: function () {
      // `this` 指向 vm 实例
      return this.message.split('').reverse().join('')
    }
  },
  created: function () {
    this.UnitList = UnitRows
    this.UnitSelected = this.UnitList.length > 0 ? this.UnitList[0].id : ''

    var val = this.UnitSelected
    this.DepartmentList = DepartmentRows.filter(function (x) {
      return x.pid === val
    })
    this.DepartmentSelected = this.DepartmentList.length > 0 ? this.DepartmentList[0].id : ''

    val = this.DepartmentSelected
    this.UserList = UserRows.filter(function (x) {
      return x.pid === val
    })
    this.UserSelected = this.UserList.length > 0 ? this.UserList[0].id : ''
  },
  watch: {
    UnitSelected: function (val) {
      this.DepartmentList = DepartmentRows.filter(function (x) {
        return x.pid === val
      })
      this.DepartmentSelected = this.DepartmentList.length > 0 ? this.DepartmentList[0].id : ''
    },
    DepartmentSelected: function (val) {
      this.UserList = UserRows.filter(function (x) {
        return x.pid === val
      })
      this.UserSelected = this.UserList.length > 0 ? this.UserList[0].id : ''
    }
  }

}
</script>

<style scoped>

</style>
