# slide-drawer

> a slide drawer component

##功能介绍
本组件旨在通过一份数据，列表渲染出一个显示样式固定的从下方弹出的抽屉，并在点击子项时判断互斥逻辑，向父组件派发相应的事件，这样父组件里只需要维护这个数据并不断传入子组件即可控制子组件的状态，
在父组件中仅需做 * 1.维护渲染子组件的数据
				 * 2.写监听点击事件后的回调函数
				 * 3.将图片资源放到合适的位置 
这3件事即可方便快捷的用起这个组件
			
##方便在哪？
* 修改抽屉里每个子项的图片，文字，选中状态，互斥逻辑十分方便，在父组件修改数据就好；
* 每个子项的点击事件，父组件写好了结构，直接添加业务代码的操作就好

##如何使用?（demo中的例子）
* in template:
```html
    <drawer
      @clicked="drawerClicked"
    ></drawer>
```
* in script:
```javascript
  components: {
    drawer
  },
  data () {
    return {
	  drawerOptions: {
	    "status": 0,                                   --未定功能
	    "message": "query ok",						   --未定功能
	    "isShow" : true,							   --组件是否显示
	    "top_btn": true,							   --是否显示顶部关闭按钮
	    "result": [                                    --用于所有的子项的数据，一个数组
		  {										
		    "id": 0,								   --子项的id
		    "name": "childlock",					   --子项的name（协议里的statueJson）
		    "text": "童锁",							   --子项的text（图片下的显示文字）
		    "setImg": "adv_childLock_set.png",		   --子项选中时的图片
		    "unsetImg": "adv_childLock_unset.png",	   --子项不选中时的图片
		    "select": true,							   --是否处于被选中状态
		    "controlable": true,					   --是否可控
		    "mutexNum": [1,3]						   --与该子项互斥的其他子项的id号
		  },
		  {											   --另一个子项的数据，每个子项都单独写一份状态数据
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
	  // 在此处添加子项被互斥或不可控的处理操作
    },
    childlockClicked() {
	  // 在此处添加子项点击的处理操作
    },
    dryClicked() {
	  // 在此处添加子项点击的处理操作
    },
    energySaveClicked() {
	  // 在此处添加子项点击的处理操作
    },
    nightWashClicked() {
	  // 在此处添加子项点击的处理操作
    },
    quietClicked() {
	  // 在此处添加子项点击的处理操作
    }
  }
```
*因为使用webpack来打包调试，图片资源处理的不好，请统一放在与 src 平级的 static/image 文件夹里
