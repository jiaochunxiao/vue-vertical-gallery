# vertical-gallery

> vue vertical-gallery components

## 线上演示地址

[demo](https://jiaochunxiao.github.io/vue-vertical-gallery/)

## 使用说明

```
<template>
    <div id="app">
        <div class="image-gallery">
             <vertical-gallery :itemHeight='120'>
                <div class="item"
                      v-for="(item, index) in imgs">
                    <img class="img-item" :src="item" alt="" />      
                </div>
             </vertical-gallery>
        </div>
    </div>
</template>

<script>
<!-- 引入组件 -->
import VerticalGallery from './components/VerticalGallery';

export default {
    name: 'App',
    data() {
        return {
            imgs: [
                require('./assets/2.jpeg'),
                require('./assets/3.jpeg'),
                require('./assets/4.jpeg'),
                require('./assets/2.jpeg'),
                require('./assets/3.jpeg'),
                require('./assets/4.jpeg')
            ]
        }
    },
    components: {
        VerticalGallery
    }
};

// 参数说明
itemHeight: 即每个item的高度，注意此处的item应该是组成 gallery中显示的每个单独的模块的高度，包含margin, padding, border等，否则计算可能会出错。
```

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
