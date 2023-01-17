## ts 文件不能识别Vue文件
### 关于Vue3+Typescript import vue 文件报红问题
> 这个问题目前已经有很多文章提出了正确的解决方案，即增加 shims-vue.d.ts 文件来解决
```ts
/* eslint-disable */
declare module '*.vue' {
  import type { DefineComponent } from 'vue'
  const component: DefineComponent<{}, {}, any>
  export default component
}
```

但是其实在VueCli创建的项目中其实是默认带 上这个文件及代码的，但是仍然会报红，

其实是因为虽然带了，但是 tsconfig.json 内并没有成功配置上这个文件
```json
{
  "extends": "@vue/tsconfig/tsconfig.web.json",
  "include": [
    "env.d.ts", 
    "src/**/*", 
    "src/**/*.vue"
  ],
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
  },

  "references": [
    {
      "path": "./tsconfig.config.json"
    }
  ]
}

```

默认的配置只匹配了src下一级及以后的目录内的文件（猜测，实际待解答），而 shims-vue.d.ts 文件在src目录下导致无法匹配，所以在第一行加上ts文件检测就可以了
```json
{
  "extends": "@vue/tsconfig/tsconfig.web.json",
  "include": [
    "src/*.ts",
    "env.d.ts", 
    "src/**/*", 
    "src/**/*.vue"
  ],
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
  },

  "references": [
    {
      "path": "./tsconfig.config.json"
    }
  ]
}

```