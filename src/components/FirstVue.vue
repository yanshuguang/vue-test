<template>

  <div>
    <h2>输出值：{{ result }}</h2>
    <button @click="goback">返回</button>
    <button @click="changeData">改变</button>
    <h3>{{ message }}</h3>
    <p>Original message: "{{ message }}"</p>
    <p>Computed reversed message: "{{ reversedMessage }}"</p>

    <ul>
      <li v-for="(item,index) in items" :key="item.message">
        {{ index }}+++++{{ item.message }}
      </li>
    </ul>

  </div>

</template>

<script>
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
      }
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
  }
}
</script>

<style scoped>

</style>
