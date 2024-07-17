**效果图**

<p>
    <img src="https://img.picui.cn/free/2024/07/17/66977d3172305.png" alt="react.png" title="react.png" />
</p>

### 一，项目描述

- 基于 vue2+datav 的基础大屏版本
- 已经做了适配，可以放心使用
- 项目需要按 f11 全屏展示
- 注意，vue2 已经不在维护了，建议 vue3+ts 开发，下方有 vue3 的 github 地址

友情链接：

1.  [vue2 官方文档](https://v2.cn.vuejs.org/)
2.  [DataV 官方文档](http://datav.jiaminghi.com/guide/)
3.  [echarts 实例](https://echarts.apache.org/examples/zh/index.html)，[echarts API 文档](https://echarts.apache.org/zh/api.html#echarts)
4.  [vue3 可视化大屏地址！！强烈建议 vue3 开发](https://github.com/huwenwu2017/vue3-datav)

### 二，文件描述

| 文件                        | 作用/功能                  |
| --------------------------- | -------------------------- |
| main.js                     | 入口文件，项目的开始       |
| app.js                      | 根组件,路由配置            |
| src/views/IndexData.vue     | 主架构组件，相当于大屏骨架 |
| src/views/IndexData 1~9.vue | 大屏里的每个小模块         |
| src/views/IndexShipei.vue   | 兼容组件                   |

### 三，大屏兼容组件

通过插槽的方式，将大屏内容加入到容器组件里去，摒弃了 vw，rem 的兼容方式，更换了缺点更少的 css3：scale 方案，对更多分辨率的设备更友好

```html
<template>
  <div class="ScreenAdapter" :style="style">
    <slot />
  </div>
</template>
<script>
  export default {
    //参数注入
    props: {
      width: {
        type: String,
        default: "1920",
      },
      height: {
        type: String,
        default: "1080",
      },
    },
    data() {
      return {
        style: {
          width: this.width + "px",
          height: this.height + "px",
          transform: "scale(1) translate(-50%, -50%)",
        },
      };
    },
    mounted() {
      this.setScale();
      window.onresize = this.Debounce(this.setScale, 1000);
    },
    methods: {
      Debounce: (fn, t) => {
        const delay = t || 500;
        let timer;
        return function () {
          const args = arguments;
          if (timer) {
            clearTimeout(timer);
          }
          const context = this;
          timer = setTimeout(() => {
            timer = null;
            fn.apply(context, args);
          }, delay);
        };
      },
      // 获取放大缩小比例
      getScale() {
        const w = window.innerWidth / this.width;
        const h = window.innerHeight / this.height;
        return w < h ? w : h;
      },
      // 设置比例
      setScale() {
        this.style.transform =
          "scale(" + this.getScale() + ") translate(-50%, -50%)";
      },
    },
  };
</script>
<style scoped>
  .ScreenAdapter {
    transform-origin: 0 0;
    position: absolute;
    left: 50%;
    top: 50%;
    transition: 0.1s;
  }
</style>
```

### 四，外层容器

在项目中，src/views/IndexData.vue 文件是初始文件，大屏里的内容都在这里面填充，这相当于是一个骨架，至关重要
而 IndexShipei 组件则是适配组件组件，在里面代码里有介绍

```html
<template>
  <!-- 全屏容器 -->
  <IndexShipei>
    <!-- 通过调用适配组件，通过插槽的方式将整个大屏传入做适配 -->
    <dv-border-box-11 title="香蕉麻花皮演示" style="background-color: black;">
      <!-- 我这里将页面分为上中下三块，这是第一块 -->
      <div class="box">
        <!-- 在里面在分成左中右3块 -->
        <div class="box1" style="padding-top: 40px;">
          <dv-border-box-12>
            <IndexData1 />
          </dv-border-box-12>
        </div>
        <div class="box1" style="padding-top: 40px;">
          <dv-border-box-2>
            <IndexData2 />
          </dv-border-box-2>
        </div>
        <div class="box1" style="padding-top: 40px;">
          <dv-border-box-10>
            <IndexData3 />
          </dv-border-box-10>
        </div>
      </div>
      <!-- 第二块 -->
      <div class="box">
        <!-- 在里面在分成左中右3块 -->
        <div class="box1">
          <dv-border-box-9>
            <IndexData4 />
          </dv-border-box-9>
        </div>
        <div class="box1">
          <dv-border-box-8>
            <IndexData5 />
          </dv-border-box-8>
        </div>
        <div class="box1">
          <dv-border-box-7>
            <IndexData6 />
          </dv-border-box-7>
        </div>
      </div>
      <!-- 第三块 -->
      <div class="box">
        <!-- 在里面在分成左中右3块 -->
        <div class="box1">
          <dv-border-box-2>
            <IndexData7 />
          </dv-border-box-2>
        </div>
        <div class="box1">
          <dv-border-box-3>
            <IndexData8 />
          </dv-border-box-3>
        </div>
        <div class="box1">
          <dv-border-box-8>
            <IndexData9 />
          </dv-border-box-8>
        </div>
      </div>
    </dv-border-box-11>
  </IndexShipei>
</template>
<script>
  import IndexShipei from "./IndexShipei.vue";
  import IndexData1 from "./IndexData1.vue";
  import IndexData2 from "./IndexData2.vue";
  import IndexData3 from "./IndexData3.vue";
  import IndexData4 from "./IndexData4.vue";
  import IndexData5 from "./IndexData5.vue";
  import IndexData6 from "./IndexData6.vue";
  import IndexData7 from "./IndexData7.vue";
  import IndexData8 from "./IndexData8.vue";
  import IndexData9 from "./IndexData9.vue";
  export default {
    data() {
      return {
        key: 1,
        config: {
          //传入组件数据
        },
      };
    },
    methods: {},

    mounted() {},
    components: {
      IndexData1,
      IndexData2,
      IndexData3,
      IndexData4,
      IndexData5,
      IndexData6,
      IndexData7,
      IndexData8,
      IndexData9,
      IndexShipei,
    },
  };
</script>
<style scoped>
  .box1 {
    width: 620px;
    height: 340px;
  }

  .box {
    display: flex;
    justify-content: space-between;
    width: 98%;
    margin: auto;
  }
</style>
```

### 五，其余

项目是个人写的基础款作品，开始的时候本来想写的是一个全面的作品，但是后续考虑到怕项目太臃肿，所以只写了基础版，虽然是基础版
但是该有的基本上都有了，完全可以作为正式项目来使用，后续在往里面添加功能也是非常简单的。
