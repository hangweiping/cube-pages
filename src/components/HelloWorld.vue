<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <a :[names]="url">aaaa</a>
    <img :[sss]="url" alt />

    <div id="demo">
      姓：<input type="text" placeholder="firstName" v-model="firstName" />
      <br />
      名：<input type="text" placeholder="lastName" v-model="lastName" /><br />
      姓名1(单向):
      <input type="text" placeholder="FullName1" v-model="fullName1" />
      <br />
      姓名2(双向):
      <input type="text" placeholder="FullName3" v-model="fullName3" />
      <br />
      {{ fullName3 }}
      <button @click="changeName()">点击改变</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String,
  },
  data() {
    return {
      names: 'href',
      sss: 'src',
      url: '/img/test.png',

      firstName: 'A',
      lastName: 'B',
      fullName2: 'A B',
    };
  },
  computed: {// 计算属性相当于data里的属性
    // 什么时候执行：初始化显示/ 相关的data属性发生变化
    fullName1() { // 计算属性中的get方法，方法的返回值就是属性值
      return `${this.firstName} ${this.lastName}`;
    },

    fullName3: {
      get() { // 回调函数 当需要读取当前属性值是执行，根据相关数据计算并返回当前属性的值
        return `${this.firstName} ${this.lastName}`;
      },
      set(val) { // 监视当前属性值的变化，当属性值发生变化时执行，更新相关的属性数据
        // val就是fullName3的最新属性值
        console.log(val);
        const names = val.split(' ');
        console.log(names);
        [this.firstName, this.lastName] = names;
      },
    },
  },
  updated() {
    console.log('updated');
  },
  methods: {
    changeName() {
      this.fullName3 = 'John Doe';
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
