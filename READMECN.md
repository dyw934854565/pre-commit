# pre-commit-with-lint

从pre-commit包fork过来的，保持了原来的pre-commit的用法，在git提交的前执行scripts中的脚本。然后添加了一个功能，是对提交的改动的文件做语法检查操作，防止提交了不规范的代码。

你也可以在scripts中加一条`lint`, 但是一个全量`lint`操作是很耗时的，也是没有必要的，所以写这个包。

# 如何使用

装包就行了，用`pre-commit-with-lint`替换原来的`pre-commit`。
```
  npm install pre-commit-with-lint --save-dev
```
如果你项目里使用了stylelint, 或者eslint，就会在提交的时候自动做lint操作了。如果没有会提醒你装包，但是不会阻止提交。

stylelint默认会检测".(s?css)|(less)$"这个正则命中的文件。

eslint默认会检测".jsx?$"这个正则命中的文件。

如果lint报错会组织本次提交。

# 修改正则字符串

默认的配置像这样，可以修改，但是注意，你一旦改了这个这个配置，但是没有装包，会直接抛错，组织提交。如果你就是想要这种效果，可以把这个默认配置拷贝到package.json里。
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

# 阻止lint操作

项目可能没加lint, 但是提交的时候会出警告。不想看到可以阻止

阻止所有
```
{
  "pre-commit": {
    "lint": "false"
  }
}
```

阻止单个
```
{
  "pre-commit": {
    "lint": {
      "eslint": "false"
    }
  }
}
```

# 增加其他操作
```
{
  "pre-commit": {
    "lint": {
      "tslint": ".ts$"
    }
  }
}
```

# 说明

增加的lint操作，其实就是。遍历改动的文件，如果命中正则，就去./node_modules/.bin/目录下去找对应的操作，没有再去全局找。然后执行对应操作，如果这个执行的有返回就会阻止提交操作。
```
    $lintname $changedfile --fix --quiet
```