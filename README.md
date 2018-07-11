# vue-elastic-tab

> A Vue.js 2.0 Tab for Web.

> 一个惯性回弹导航tab

![image](https://github.com/webFirstDog/vue-elastic-tab/blob/master/src/assets/tupianfaguang.gif)
![image](https://github.com/webFirstDog/vue-elastic-tab/blob/master/src/assets/tupianfaguang1.gif)

## Build Setup

``` bash
# install dependencies 首先安装依赖项
npm install

# serve with hot reload at localhost:8080 然后，开发环境，在本地主机上热重载服务:8080
npm run dev

# build for production with minification 生产环境，上线打包
npm run build
```

## Browser Support

Mobile terminal

## Install

```bash
npm install vue-elastic-tab -S
```

## Quick Start
```vue
<template>
  <div id="app">		
    <vue-g-huitan
      GDirection="x" 
      :GNavName="li_array" 
      :GNavLink="li_array_link"
      GNavId="tanxinNav"
      GBg="#5cadff" 
      :GMaxWithY="100" 
      :GElastic="150"></vue-g-huitan>
  </div>
</template>

<script>
export default {
  data () {
    return {
      li_array: ["前面的","world","love","china"],
      li_array_link: ["/hello","/world","/love","china"]
    }
  }
}
</script>

```
