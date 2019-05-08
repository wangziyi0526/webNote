### vuex 简装盗版地摊货

> 本人是一个逗逼的前端er 写东西的语言呢，也颇具逗逼风格，各位看官见谅

#### 啥是vuex

> Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。Vuex 也集成到 Vue 的官方调试工具 devtools extension，提供了诸如零配置的 time-travel 调试、状态快照导入导出等高级调试功能。

- 上述为vuex官网中的介绍 
- 下述为本人的逗逼理解，不一定对 但是接近吧！
  
> 你，是组件， 掌握你经济大权的人 是vuex, 当你想要用钱的时候去掌握你经济大权的人那里去拿, 但是呢, 你要是想花钱, 得通过合理的流程去通知你的vuex, 那你要是打牌赢钱了呢, 也需要通过合理的流程提交上去
  
#### 什么时候用vuex呢？

- 这是一个老生常谈的问题，啥时候用啊？我为什么要用啊？恩官方说的是便于组件之间共享状态等！
- but 我有不同见解理解方式，公司要让你出去办事情，你会自己拿钱帮着公司办么？万一不还咋办，所以还是统一在公司拿钱吧！
  
#### 怎么在vuex(公司拿钱)呢？

- 走流程！在公司办事你不得走流程么？去找财务小姐姐 说明情况等等的 
- 那在vuex中呢 怎么弄？
  
store.js(公司资源部)

```
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  state:{
    money:100000000
     <!-- 这么多钱哈哈哈 太刺激了 -->
  }
})

```

index.vue (你)
```
import { mapState } from 'vuex' // 引入它呢，能帮你映射出来资源

computed: {
  ...mapState([
    'money'
  ])
}

 <!-- 这个时候你就拿到了钱，在你的天地里面挥霍吧！但是挥霍 钱变了 得告诉财务小姐姐(vuex)，怎么告诉呢？肯定不是发微信，打电话 -->

```
#### 告诉公司(vuex)钱数变了 (moutation)

> moutation 在vuex官网中解释说 "更改 Vuex 的 store 中的状态的唯一方法是提交 mutation。Vuex 中的 mutation 非常类似于事件：每个 mutation 都有一个字符串的 事件类型 (type) 和 一个 回调函数 (handler)。这个回调函数就是我们实际进行状态更改的地方，并且它会接受 state 作为第一个参数"

不正经的时候到了

> 还是用  拿公司的钱  举例子吧
> 流程 走流程  是吧 你拿着公款，去为公司谈业务，那就涉及到花钱 或者不花钱 亦或者 把客户陪好了，客户给的小费，哈哈哈  开玩笑 总之 你因为什么吧改变了原有的在财务小姐姐哪里的money的数值(store中的state中的money)  那就用moutation去走流程

- 来走流程，
  
```
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  state:{
    money:100000000
     <!-- 这么多钱哈哈哈 太刺激了 -->
  },
  <!-- 流程第一步，和小姐姐订好了，我可能会在什么情况下用钱 -->
  moutation: {
    <!-- 购物，里面两个参数，第一个呢  就是  上述的money， 第二个n呢 官网说的是载荷 payload
      shopping么，用钱么 花钱，花store中state的money,所以这个就是第一个参数，那n呢 就是你花多少啊！ 嗯应该是这样 哈哈哈
     -->
    shopping (state, n){
      state.money -= n
    }
  }
})

```
- 那我们和财务小姐姐(store)打好招呼了，愉快的花钱吧

- index.vue  就是你
```
import { mapState } from 'vuex' // 引入它呢，能帮你映射出来资源
import { mapMoutation} from 'vuex'  // 引入它呢，能帮你映射出来当年大明湖畔的约定

computed: {
  ...mapState([
    'money'
  ])
},
<!-- 方法里，实现约定 -->
methods: {
  ...mapMutation([
    'shopping' // 将 `this.shopping()` 映射为 `this.$store.commit('shopping')`
  ])
}

```