# Sublime Text新建文件模版

1. 下载插件**SublimeTmpl**

2. SublimeTmpl内置了html、css、javascript、php、python和ruby六种类型的文件模版，文件模版保存在`Packages\SublimeTmpl\templates`，可自行修改

3. SublimeTmpl默认的快捷键：

  ```
  ctrl+alt+h html
  ctrl+alt+j javascript
  ctrl+alt+c css
  ctrl+alt+p php
  ctrl+alt+r ruby
  ctrl+alt+shift+p python
  ```

4. 进入模版目录，修改模版的办法：

  `ctrl + shift + p` -> Package Control:List Package -> 搜索Tmpl -> 点击进入

5. 自定义模版

  - 用户自定义模版统一放到`Packages/User/SublimeTmpl/templates`,优先级高于默认模版

6. 模版语法

  支持自定义变量，在Preferences -> Packages Settings -> SublimeTmpl -> Settings:User，如

  ```
  {
	"attr":{
      "author": "sharpdeep" ,
      "email": "cairuishen@gmail.com",
      "link": "http://sharpdeep.github.io",
      "date": "%Y-%m-%d %H:%M:%S",
  }
}
  ```

  在Python模版中引用

  ```
  #!/usr/bin/env python
  # -*- coding: utf-8 -*-
  # @Date    : ${date}  
  # @Author  : ${author} (${email})
  # @Link    : ${link}
  # @Date	   : ${date}

  ${2:import os}
  $1
  ```
  `$N`表示顺序，`$1`表示光标最后停留的位置

7. 添加一个新模版，以Lua为例

  Preferences -> Package settings -> SublimeTmpl

  * Settings - Menu
  add
  ```py
  {
  "caption": "Lua",
  "command": "sublime_tmpl",
  "args": {
      "type": "lua"
  }
  },
  ```

  * Settings - Commands
  add
  ```py
  {
  "caption": "Tmpl: Create lua", "command": "sublime_tmpl",
  "args": {"type": "lua"}
  },
  ```

  * Settings - Default
  add
  ```py
  "scss": {
  "syntax": "Packages/Lua/lua.tmLanguage"
  },
  ```

  * Key Bindings
  add
  ```py
  ,{
  "keys": ["ctrl+alt+l"], "command": "sublime_tmpl",
  "args": {"type": "lua"}
  }
  ```

  * 新建一个模版文件
