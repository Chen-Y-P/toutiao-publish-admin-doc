## 路由设计

| 路径                | 说明                |
| ------------------- | ------------------- |
| /                   | 首页                |
| /login              | 用户登录            |
| /article            | 文章管理            |
| /publish            | 发布头条            |
| /publish/:articleId | 修改发布头条        |
| /comment            | 评论管理            |
| /image              | 素材管理            |
| /fans               | 粉丝管理            |
| /fans/overview      | 粉丝管理 / 粉丝概况 |
| /fans/portrayal     | 粉丝管理 / 粉丝画像 |
| /fans/list          | 粉丝管理 / 粉丝列表 |
| /account            | 账户设置            |

## 自定义 ESLint 代码校验规则

大多数情况下我们使用默认规则就可以了，但有时候也需要根据团队或个人的需要进行一些规则的自定义配置。

ESLint 最初是由[Nicholas C. Zakas](http://nczonline.net/) 于 2013 年 6 月创建的开源项目。它的目标是提供一个插件化的 javascript 代码检测工具。

- [ESLint 官网](https://cn.eslint.org/)
- [ESLint 规则表](https://cn.eslint.org/docs/rules/)

项目中的 `.eslintrc.js` 文件就是 ESLint 的配置文件：

```js
module.exports = {
  root: true,
  env: {
    node: true
  },
  extends: ["plugin:vue/essential", "@vue/standard"],
  // 这里可以进行自定义规则配置
  // key：规则代号
  // value：具体的限定方式
  //   "off" or 0 - 关闭规则
  //   "warn" or 1 - 将规则视为一个警告（不会影响退出码）,只警告，不会退出程序
  //   "error" or 2 - 将规则视为一个错误 (退出码为1)，报错并退出程序
  rules: {
    "no-console": process.env.NODE_ENV === "production" ? "error" : "off",
    "no-debugger": process.env.NODE_ENV === "production" ? "error" : "off",
    "space-before-function-paren": [
      "error",
      {
        anonymous: "never",
        named: "never",
        asyncArrow: "never"
      }
    ]
    // 'semi': ['error', 'always']
  },
  parserOptions: {
    parser: "babel-eslint"
  }
};
```

其中的 `rules` 选项对象可以用来配置具体的校验规则，其中对象的 `key` 是规则代号，`value` 是规则说明。

例如：

```json
{
  "rules": {
    "semi": ["error", "always"],
    "quotes": ["error", "double"]
  }
}
```

`"semi"` 和 `"quotes"` 是 ESLint 中 [规则](https://cn.eslint.org/docs/rules) 的名称。第一个值是错误级别，可以使下面的值之一：

- `"off"` or `0` - 关闭规则
- `"warn"` or `1` - 将规则视为一个警告（不会影响退出码）
- `"error"` or `2` - 将规则视为一个错误 (退出码为 1)

这三个错误级别可以允许你细粒度的控制 ESLint 是如何应用规则（更多关于配置选项和细节的问题，请查看[配置文件](https://cn.eslint.org/docs/user-guide/configuring)）。

我们可以根据 ESLint 官方提供的规则列表进行具体的配置。