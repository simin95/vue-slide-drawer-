<template>
  <div class="hello">
    <ul class="list">
      <li v-for="(item,index) in pdata" :key="index">
        {{item.id}}+{{item.name}}
      </li>
    </ul>
    <button @click="showDrawer">弹出抽屉</button>
    <transition name="drawer-wrapper">
      <div class="drawer-container" v-show="propData.isShow">
        <div class="button-container" @click="propData.isShow=false" v-if="propData.top_btn">
          <span class="button" ></span>
        </div>
        <div class="drawer">
          <ul class="item-container">
            <li
              class="item"
              v-for="(item,index) in pdata"
              :key="index"
              @click="clickEvent(index)"
            >
              <div class="inside-box">
                <img class="img" v-show="item.select" :src=getImg(item.setImg)>
                <img class="img" v-show="!item.select" :src=getImg(item.unsetImg)>
                <span class="text">{{item.text}}</span>
              </div>
            </li>
          </ul>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>

//  测试时用这个json模拟
//  const propData = require('./mockprops.json')
export default {
  name: 'drawer',
  props: ['drawerOptions'],
  data () {
    return {
      // 传入的原始数据
//      propData: propData.
      propData: this.drawerOptions,
      // 组件里所有的子项状态
//      pdata: propData.result,
      pdata: this.drawerOptions.result,
      // 用来存当前被显示的项的id
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
      this.propData.isShow = !this.propData.isShow
    },
    // 拿到图片url地址并转为style格式绑定到item
    getImg(url) {
//      console.log(`/static/image/${url}`)
      return `/static/image/${url}`
    },
    // 点击事件，里面包含：
    // 1.点击图片切换背景图片，传出本子元素的点击事件名，互斥逻辑也添加在此，用id做区分，另有元素是否可控判断
    // 2.不互斥：修改背景，传出点击事件；互斥/不可控：传出互斥事件名
    clickEvent(index,event) {
      console.log("selectId: " + this.selectId)
//      console.log(this.pdata[index].mutexNum)
      // 是否被互斥的标志位 被互斥true 不被互斥false
      let isMutex = this.haveSameItem(this.selectId, this.pdata[index].mutexNum)
      if (this.pdata[index].controlable === false){
        console.log("当前按钮处于不可控状态")
      } else if (isMutex) {
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
      // 传出点击事件，带参数：1.事件名 2.是否被互斥（true被互斥） 3.是否可控（true可控）
      this.$emit('clicked',[this.pdata[index].name, isMutex, this.pdata[index].controlable])
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
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" rel="stylesheet/stylus">
@import "slideDrawer";

</style>
