# vue-aliplayer

基于 aliplayer 封装 vue 视频播放器组件，相较于在社区找到的其他 vue-aliplayer 插件，具有以下特点：

* 兼容 aliplayer sdk 2.8.2 版本
* 视频自适应居中
* 修复因为 `skinLayout` 导致的控件不显示的问题
* 修复部分情况下，播放器脚本加载两次，初始化两个播放器的问题

## 接口文档以及示例

[阿里云播放器官方文档](https://help.aliyun.com/document_detail/125572.html)

[官方示例](https://player.alicdn.com/aliplayer/presentation/index.html)

## 组件使用

将 `components/Aliplayer.vue` 拷贝到项目中

```html
<template>
  <div>
    <ali-player
      ref="player"
      source="//player.alicdn.com/video/editor.mp4"
      width="100%"
      height="500px"
      :preload="true"
      :useH5Prism="true"
      @pause="onPause">
    </ali-player>
  </div>
</template>
```

```js
<script>
import Aliplayer from "../components/Aliplayer"

export default {
  components: {
    "ali-player": Aliplayer
  },
  data() {
    return {
      
    }
  },
  methods: {
    onPause() {
      console.log('pause')
      if (this.$refs.player) {
        console.log(this.$refs.player.getCurrentTime())
      }
    }
  },
}
</script>
```