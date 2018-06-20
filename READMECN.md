# pre-commit-with-lint

##介绍

从pre-commit包fork过来的，保持了原有的pre-commit的用法，在git提交前执行scripts中被指定的脚本。

**新增**了对本次提交中**改动的文件**做语法检查操作的功能，防止不规范的代码被提交。

与在scripts中添加`lint`相比,节省了检查全部文件的时间。

# 如何使用

安装 `pre-commit-with-lint` 替换 `pre-commit`。

```
  npm install pre-commit-with-lint --save-dev
```

如果项目中使用了stylelint或者eslint，那么提交的时会自动进行lint操作。如果没有则会提醒装包，但是不会阻止提交。

stylelint 默认检测 ".(s?css)|(less)$" 正则命中的文件。

eslint 默认检测 ".jsx?$" 正则命中的文件。

如果lint报错会阻止本次提交。

## 修改配置

默认配置如下，可以根据项目需求进行修改。需要注意的是，一旦修改了配置后，如果没有安装相应的包，会直接报错阻止提交。
因此可以通过这个特性来提醒项目成员安装指定包。

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

## 取消lint操作

项目中不需要lint时，可以关闭lint功能来去除警告。

```
{
  "pre-commit": {
    "lint": "false"   //取消所有lint
  }
}

{
  "pre-commit": {
    "lint": {
      "eslint": "false"   //取消指定lint
    }
  }
}
```

## 增加其他操作

```
{
  "pre-commit": {
    "lint": {
      "tslint": ".ts$"
    }
  }
}
```

## 说明

lint操作是在scripts执行之后进行的，`pre-commit`默认执行`test`。如果不需要可以配置成空数组

```
{
  "pre-commit": {
    "run": []
  }
}
```
