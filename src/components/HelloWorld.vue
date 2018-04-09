<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <drawer
      :drawerOptions="this.drawerOptions"
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
      msg: 'Welcome to Your Vue.js App',
      drawerOptions: {
        "status": 0,
        "message": "query ok",
        "isShow" : true,
        "top_btn": true,
        "result": [
          {
            "id": 0,
            "name": "childlock",
            "text": "童锁",
            "setImg": "adv_childLock_set.png",
            "unsetImg": "adv_childLock_unset.png",
            "select": true,
            "controlable": true,
            "mutexNum": [1,3]
          },
          {
            "id": 1,
            "name": "dry",
            "text": "烘干",
            "setImg": "adv_dry2_set.png",
            "unsetImg": "adv_dry2_unset.png",
            "select": false,
            "controlable": true,
            "mutexNum": [0,2,4]
          },
          {
            "id": 2,
            "name": "energySave",
            "text": "节能",
            "setImg": "adv_energySave_set.png",
            "unsetImg": "adv_energySave_unset.png",
            "select": true,
            "controlable": true,
            "mutexNum": [1,3]
          },
          {
            "id": 3,
            "name": "nightWash",
            "text": "夜间洗",
            "setImg": "adv_nightWash_set.png",
            "unsetImg": "adv_nightWash_unset.png",
            "select": false,
            "controlable": true,
            "mutexNum": [0,2,4]
          },
          {
            "id": 4,
            "name": "quiet",
            "text": "静音",
            "setImg": "adv_quiet_set.png",
            "unsetImg": "adv_quiet_unset.png",
            "select": true,
            "controlable": true,
            "mutexNum": [1,3]
          }
        ]
      }
    }
  },
  methods: {
    drawerClicked(arr) {
      console.log("drawerClicked")
      if (arr[1] === true || arr[2] === false) {
        this.mutexed()
//        console.log("该项被互斥或不可控")
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
      alert("该项被互斥或处于不可控状态")
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
