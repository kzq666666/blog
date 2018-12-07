---
title: "Vue3"
date: 2018-12-04T18:21:14+08:00
showDate: true
draft: false
tags: ["vue","vue3.0"]
---
## 组件传值

```
App.vue:
        <HelloWorld msg="HelloWorld"/>
        
HelloWorld.vue:
                <script>
                export default {
                name: 'HelloWorld',
                props: {
                    msg: String
                }
                }
                </script>
```
