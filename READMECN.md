# pre-commit-with-lint

## 介绍

保留 pre-commit 原有可以在git提交前执行scripts中被指定的脚本的用法。

**新增**对当前提交中**改动的文件**做语法检查操作的功能，防止不规范的代码被提交。

与在scripts中添加`lint`相比,节省了检查全部文件的时间。

## 如何使用

安装 `pre-commit-with-lint` 替换 `pre-commit`。

```
  npm install pre-commit-with-lint --save-dev
```

如果项目中使用了stylelint或者eslint，提交的时候会自动进行lint操作。如果没有，则会提醒装包，但是不会阻止提交。

stylelint 默认检测 ".(s?css)|(less)$" 正则命中的文件。

eslint 默认检测 ".jsx?$" 正则命中的文件。

如果lint报错会阻止本次提交。

## 修改配置

默认配置如下，可以根据项目需求进行修改。

```
{
  "pre-commit": {
    "lint": {
      "stylelint": ".(s?css)|(less)$",
      "eslint": ".jsx?$"
    }
  }
}
```

## 自定义配置

```
{
  "pre-commit": {
    "lint": {
      "tslint": ".ts$"
    }
  }
}
```

需要注意的是，一旦修改了配置后，如果没有安装相应的包，会直接报错阻止提交。因此可以通过这个特性来提醒项目成员安装指定包。

## 禁用lint

项目中不需要lint时，可以关闭lint功能去除警告。

```
{
  "pre-commit": {
    "lint": "false"   //禁用所有lint
  }
}

{
  "pre-commit": {
    "lint": {
      "eslint": "false"   //禁用指定lint
    }
  }
}
```



## 禁用pre-commit

lint操作是在scripts执行之后进行的，`pre-commit`默认执行`test`。如果不需要可以配置成空数组

```
{
  "pre-commit": {
    "run": []
  }
}
```
