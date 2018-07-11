# vue-elastic-tab

> A Vue.js 2.0 Tab for Web.

> 一个惯性回弹导航tab

![image](./src/assets/tupianfaguang.gif)
![image](./src/assets/tupianfaguang1.gif)

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