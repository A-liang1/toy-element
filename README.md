# toy-element（Vue3 + Ts 组件库搭建）

实现一个自己的组件库，同时深入学习 element-ui

## 一、搭建 monorepo 环境

> 使用 pnpm 安装包速度快，磁盘空间利用率高效，使用 pnpm 可以建立 monorepo 环境，
>
> so~ 我们这里使用 pnpm workspace 来实现 monorepo。

```
npm install pnpm -g   #全局安装pnpm
pnpm init   #初始化package.json配置文件 私有库
pnpm install vue typescript -D  #全局下添加依赖
```

> 在编写组件库的时候可能用到 vue 和 ts 中一些模块，比如说响应式系统，但是这些模块都在 node_modules 的.pnpm 下，
>
> 所以我们需要在 .npmrc 中配置一下,shamefully-hoist = true 修饰的提升,将 pnpm 下的依赖提升到外边这个目录下也就是 node_modules，这样我们就可以在项目中直接使用了。

```
pnpm install # 再安装一次
```

> 初始化一个 ts 的配置文件

```
pnpm tsc --init
```

```
# 在tsconfig.json中
"compilerOptions": {
    "module": "ESNext", // 打包模块类型ESNext
    "declaration": false, //默认不要声明文件
    "noImplicitAny": false, //支持类型不标注可以默认any
    "removeComments": true, //删除注释
    "moduleResolution": "node", //按照node模块来解析
    "esModuleInterop": true, //支持es6，commonjs模块
    "jsx": "preserve", //jsx 不转
    "noLib": false, //不处理类库
    "target": "es6", //遵循es6版本
    "sourceMap": true,
    "lib": ["ESNext", "DOM"], //编译时用的库
    "allowSyntheticDefaultImports": true, //允许没有导出的模块中导入
    "exporimentalDecorators": true, //装饰器语法
    "forceConsistentCasingInFileNames": true, //强制区分大小写
    "resolveJsonModule": true, //解析json模块
    "strict": true, //是否启动严格模式
    "skipLibCheck": true //跳过类库检查
  },
  "exclude": ["node_modules", "**/__tests__", "dist/**"] //排除掉哪些类库
```
