<p align="center">
    <a href="https://www.iviewui.com">
        <img width="200" src="https://file.iviewui.com/logo.svg">
    </a>
</p>

# M-Admin

[![](https://img.shields.io/travis/iview/iview-admin.svg?style=flat-square)](https://travis-ci.org/iview/iview-admin)
[![vue](https://img.shields.io/badge/vue-2.5.13-brightgreen.svg?style=flat-square)](https://github.com/vuejs/vue)
[![iview ui](https://img.shields.io/badge/iview-2.8.0-brightgreen.svg?style=flat-square)](https://github.com/iview/iview)
[![npm](https://img.shields.io/npm/l/express.svg)]()


## 当前版本：v0.0.1

## 安装依赖

```bush
npm install
```

## 开发环境预览

```bush
npm run dev
```

### 生产环境打包

```bush
npm run build
```

## 简介

&emsp;&emsp;M-Admin基于iview-admin简单改造，主要提供通过iview-admin起步建立一个后台的基本用法，并对页面初始化、组件引入和使用进行简单说明。iView admin是基于Vue.js，搭配使用[iView](https://www.iviewui.com) UI组件库形成的一套后台集成解决方案，由TalkingData前端可视化团队部分成员开发维护。iView admin遵守iView设计和开发约定，风格统一，设计考究，并且更多功能在不停开发中。
如果您想查看iview-admin的更新动态，您可以到[更新日志](https://github.com/iview/iview-admin/releases)查看了解最新更新；如果您是新手，想快速入手iview-admin，您可以到[使用教程](https://github.com/iview/iview-admin/wiki)查看讲解；如果您想在线体验iview-admin，您可以到[在线访问](https://iview.github.io/iview-admin)体验。

## 使用

### 新建菜单及页面

#### 新建左边菜单

    例：想要创建菜单

        测试页
           ├── 测试页1
           ├── 测试页2
    1. 新建文件夹及页面

    在`src/views/`目录下，新建`demo`文件夹，`demo`中新建`page1.vue`和`page2.vue`，具体新建页面方法见下面新建页面

    2. 在`/src/router/router.js`中，数组`appRouter`中添加菜单配置，例：

    ```javascript
        [{
            // hash后一级目录
            path: '/demo',
            // 菜单图标 icon值参见 https://www.iviewui.com/components/icon
            icon: 'thumbsup',
            // 尽量语义化，易辨认，无特殊含义
            name: 'demo',
            // 一级菜单标题
            title: '测试页',
            // 默认使用Main
            component: Main,
            // 二级菜单
            children: [
                {
                    // hash后二级目录
                    path: 'page1',
                    // 二级菜单标题及标签标题
                    title: '测试页1',
                    // 尽量语义化，易辨认，无特殊含义
                    name: 'demo-page1',
                    // 引入页面组件，括号中路径以@开头，相对src/的路径
                    component: () => import('@/views/demo/page1.vue')
                },
                { path: 'page2', title: '测试页2', name: 'demo-page2', component: () => import('@/views/demo/page2.vue') }
            ]
        }]
    ```

#### 新建页面

    1. 新建pagename.vue文件
    2. 页面基本结构

    ```javascript
        <style lang="less">
        @import "../../styles/common.less";
        </style>
        <template>
            <div class="home-main">
                这里是demo页1
            </div>
        </template>

        <script>

        export default {
            name: 'page1',
            components: {

            },
            data () {
                return {

                };
            },
            computed: {

            },
            methods: {

            }
        };
        </script>

    ```

- `style`： style标签下可以直接写样式，或者import其他样式文件
- `template`：在`<div class="home-main">`内部添加其他DOM元素或者组件
- `script`：变量定义可以在script标签下，方法定义放在`methods`中，方法调用可以`template`行内或者在`created`中，`created`可以理解为页面初始化完成，`DOM`元素加载之前的那一段时间，`mounted`代表页面`DOM`也已经加载完成，更多相关问题可参照[VUE官网](https://cn.vuejs.org/)

#### 异步请求

1. 在`srcipt`标签中引入axios：`import axios from 'axios';`
2. 发起请求：

```javascript
/*
* get请求，第二个参数为`{params: {id: 123}}`
* post请求，第二个参数为`{id: 123}`
*/
axios.get(url, {params: {}})
    .then(res => {
        let _res = res.data
    })
```

## License

[MIT](http://opensource.org/licenses/MIT)

Copyright (c) 2016-present, iView
