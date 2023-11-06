## Preface

The project is the front-end part of the front-end separation project, and the back-end project mall address([https://github.com/Georgezxh/Micro-Service-E-commerce-System](https://github.com/Georgezxh/Micro-Service-E-commerce-System)) 

## Introduction

'mall-admin-web' is a front-end project of the back-end management system of e-commerce, based on Vue+Element implementation. It mainly includes commodity management, order management, member management, promotion management, operation management, content management, statistical reports, financial management, rights management, setting and other functions.

### Presentation


![image](https://github.com/Georgezxh/Mall-admin-web/assets/50438846/8f423e45-cb37-405d-8482-7e3afd97796b)


### Technology selection

| Technology        |  Explain                 | Website                                                         |
| ----------------- | ---------------------    | ------------------------------------------------------------ |
| Vue               | Front-end frame          | [https://vuejs.org/](https://vuejs.org/)                     |
| Vue-router        | Route frame              | [https://router.vuejs.org/](https://router.vuejs.org/)       |
| Vuex              | Global state management framework      | [https://vuex.vuejs.org/](https://vuex.vuejs.org/)           |
| Element           | Front-end UI frame       | [https://element.eleme.io/](https://element.eleme.io/)       |
| Axios             | Front-end http frame     | [https://github.com/axios/axios](https://github.com/axios/axios) |
| v-charts          | Chart framework based on Echarts | [https://v-charts.js.org/](https://v-charts.js.org/)         |
| Js-cookie         | cookie management tool        | [https://github.com/js-cookie/js-cookie](https://github.com/js-cookie/js-cookie) |
| vue-element-admin | Project scaffolding reference        | [https://github.com/PanJiaChen/vue-element-admin](https://github.com/PanJiaChen/vue-element-admin) |

### 项目布局

``` lua
src -- Source code directory
├── api -- axios request definition
├── assets -- Static image resources files
├── components -- Universal component package
├── icons -- svg pics
├── router -- vue-route configuration
├── store -- vuex status management
├── styles -- Global css style
├── utils -- Tool class
└── views -- Front-end oage
    ├── home -- Home page
    ├── layout -- Universal page loading framework
    ├── login -- Login page
    ├── oms -- Order module page
    ├── pms -- Product module page
    └── sms -- Marketing module page
```

## Build steps
- `npm install`, download dependent dependencies
- `npm run dev`
- Visit address：[http://localhost:8090](http://localhost:8090) 

