<template>
  <div id="app">
    <div id="nav">
        <p><router-link to="/">1.Home</router-link></p>
        <p><router-link to="/about">2.About</router-link></p>
        <p><a href="#" @click="gotoSubReact" style="marin: 0 0 0 10px">3.跳转到sub-react</a></p>
        <p><a href="#" @click="modifyUserName" style="marin: 0 0 0 30px">4.修改公共vuex中用户名为李四</a></p>
    </div>
    <div>
      从vuex的global module的state： {{ JSON.stringify(user) }}
    </div>
    <div>
      <input type='input' placeholder="请输入"/>
    </div>
    <router-view/>
  </div>
</template>
<script>
import { mapState } from 'vuex'
import store from './store'
export default {
  computed: {
    // 通过global获取user的信息
    ...mapState('global', {
      user: state => state.user
    })
  },
  methods: {
    gotoSubReact () {
      history.pushState({ info: 77777 }, 'sub-react-title', '/sub-react') // 三个参数分别为携带参数，title,路由地址
    },
    modifyUserName () {
      store.commit('global/setGlobalState', { user: '李四' })
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

</style>
