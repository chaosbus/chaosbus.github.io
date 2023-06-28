# VSCode使用技巧汇总


由于日常经常使用**VSCode**，使用过程中会遇到一些问题或好用的插件，因此记录一下。

虽然没有**PyCharm**方便，但是轻啊，响应速度快很多，毕竟很多实用的高级功能在社区版是没有的:cry:（remote WSL/SSH）。

<!--more-->

## 一、设置文件头注释

**VSCode**可以像**PyCharm**那样为文件添加自定义文件头注释，虽然还是没有后者方便，需要手工触发操作一下。

1. 设置用户代码片断

   > 【File】-【Preferences】-【User Snippets】

   ![image-20230613010829657](https://images.origins.top/posts/image-20230613010829657.png)

2. 在弹出窗口中输入代码类型，此处以**Python**为例

   ![image-20230613011122220](https://images.origins.top/posts/image-20230613011122220.png)

3. 编辑自己想要的格式

   例：

   ```json
   {
    // Place your snippets for python here. Each snippet is defined under a snippet name and has a prefix, body and 
    // description. The prefix is what is used to trigger the snippet and the body will be expanded and inserted. Possible variables are:
    // $1, $2 for tab stops, $0 for the final cursor position, and ${1:label}, ${2:another} for placeholders. Placeholders with the 
    // same ids are connected.
    // Example:
    // "Print to console": {
    //  "prefix": "log",
    //  "body": [
    //   "console.log('$1');",
    //   "$2"
    //  ],
    //  "description": "Log output to console"
    // }
    "HEADER": {
     "prefix": "fd",
     "body": [
      "#!/usr/bin/env python",
      "#-*- coding: utf-8 -*-",
      "\"\"\"",
      "@File        : $TM_FILENAME",
      "@CreateTime  : $CURRENT_YEAR-$CURRENT_MONTH-$CURRENT_DATE $CURRENT_HOUR:$CURRENT_MINUTE:$CURRENT_SECOND",
      "@Version     : ",
      "@Author      : Joe",
      "@Description : ",
      "\"\"\"",
      "",
     ]
    }
   }
   ```

   **prefix**的value值为生成文件头注释的触发词。此处为`fd`

   ![Code_NYwvw3YRVW](https://images.origins.top/posts/Code_NYwvw3YRVW.gif)

   其中变量参考[VSCode官方文档](https://code.visualstudio.com/docs/editor/userdefinedsnippets#_snippet-syntax)

## 二、debug到第三方包（非本地代码）中添加断点

默认的`.vscode/launch.json`配置如下：

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Python: 当前文件",
      "type": "python",
      "request": "launch",
      "program": "${file}",
      "console": "integratedTerminal",
      "justMyCode": true,
      "env": {
      }
    }
  ]
}
```

其中的`justMyCode`改为`false`即可。

