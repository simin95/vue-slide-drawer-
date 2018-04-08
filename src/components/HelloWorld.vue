<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <drawer
      @clicked="drawerClicked"
    ></drawer>
  </div>
</template>

<script>
  import drawer from './slideDrawer.vue'
export default {
  name: 'HelloWorld',
  components: {
    drawer
  },
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  methods: {
    drawerClicked(arr) {
      console.log("drawerClicked")
      if (arr[1] === true) {
        this.mutexed()
//        console.log("该项被互斥")
      } else {
        switch (arr[0]) {
          case 'childlock':
            this.childlockClicked()
          break;
          case 'dry':
            this.dryClicked()
          break;
          case 'energySave':
            this.energySaveClicked()
          break;
          case 'nightWash':
            this.nightWashClicked()
          break;
          case 'quiet':
            this.quietClicked()
          break;
          default:
            console.log('传值错误，检查name是否正确')
          break;
        }
      }
    },
    mutexed() {
      alert("该项被互斥")
    },
    childlockClicked() {
      alert("童锁被点击")
    },
    dryClicked() {
      alert("烘干被点击")
    },
    energySaveClicked() {
      alert("节能被点击")
    },
    nightWashClicked() {
      alert("夜间洗被点击")
    },
    quietClicked() {
      alert("静音被点击")
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
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
