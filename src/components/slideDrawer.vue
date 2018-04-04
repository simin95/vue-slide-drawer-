<template>
  <div class="hello">
    <ul class="list">
      <li v-for="(item,index) in pdata" :key="index">
        {{item.id}}+{{item.name}}
      </li>
    </ul>
    <button @click="showDrawer">弹出抽屉</button>
    <transition name="drawer-wrapper">
      <div class="drawer-container" v-show="isShow">
        <div class="drawer">
          <ul class="item-container">
            <li
              class="item"
              v-for="(item,index) in pdata"
              :key="index"
              @click="toggleImage(index)"
            >
              <img class="img" v-show="item.select" :src=getImg(item.setImg)>
              <img class="img" v-show="!item.select" :src=getImg(item.unsetImg)>
              <span class="text">{{item.name}}</span>
            </li>
          </ul>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
  const propData = require('./mockprops.json')
export default {
  name: 'drawer',
  props: [],
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      isShow: true,
      setImg: false,
      pdata: propData.result,
      selectId: []
    }
  },
  created() {
    // 初始化selectId这个数组：
    console.log("start created")
    for(var item of this.pdata) {
      console.log(item)
      if (item.select === true)
        this.selectId.push(item.id)
    }
    console.log("selectId: " + this.selectId)
  },
//  watch: {
//    selectId: function (val, oldval) {}
//  },
  methods: {
    showDrawer() {
      this.isShow = !this.isShow
    },
    // 拿到图片url地址并转为style格式绑定到item
    getImg(url) {
//      console.log(`/static/image/${url}`)
      return `/static/image/${url}`
      //
    },
    // 点击图片切换背景，互斥逻辑也添加在此，用id做区分。
    // 不互斥：修改背景，传出点击事件；互斥/不可控：提示信息，不传出事件
    toggleImage(index) {
      console.log("selectId: " + this.selectId)
//      console.log(this.pdata[index].mutexNum)
      if (this.pdata[index].controlable === false){
        console.log("当前按钮处于不可控状态")
      } else if (this.haveSameItem(this.selectId, this.pdata[index].mutexNum)) {
        console.log("当前按钮被其他按钮互斥，id是" + this.selectId)
      } else {
        this.pdata[index].select = !this.pdata[index].select;
        // 如果index在selectId里有则删去，没有则加上
        let inSelectId = this.selectId.indexOf(index);
        if (inSelectId >= 0)
          this.selectId.splice(inSelectId,1)
        else
          this.selectId.push(index)
        console.log("index: "+index)
        console.log("selectId:"+this.selectId)

      }
    },
    /**
     * @desc 判断两个数组是否有相同元素
     * input: array1, array2
     * output: boolean
     */
    haveSameItem(arr1, arr2) {
      for(var item of arr1){
        if(arr2.indexOf(item) >= 0)
          return true;
      }
      return false;
    },

    event1() {
      alert("按钮1事件已触发")
    },
    event2() {
      alert("按钮222事件已触发")
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" rel="stylesheet/stylus">
@import "slideDrawer";

</style>
