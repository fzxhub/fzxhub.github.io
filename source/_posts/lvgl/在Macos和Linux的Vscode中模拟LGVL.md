---
title: 在Macos和Linux的Vscode中模拟LGVL
date: 2021-07-32
author: fzxhub
cover: true
img: 
summary: LGVL是一个开源的嵌入式GUI，可以方面进行嵌入式的图形界面开发。
categories: lgvl
tags:
  - lgvl
  - gui
  - 嵌入式
  - vscode
---

## 资源链接

- **博客网站：**[**fzxhub**](https://fzxhub.com)
- **代码仓库：**[**fzxhub/lvglsim_vscode**](https://github.com/fzxhub/lvglsim_vscode)

## 简介
LGVL是一个开源的嵌入式GUI，可以方面进行嵌入式的图形界面开发。

## Linux/Macos在vscode中模拟LGVL步骤

1. 确保PC安装了gcc、make、gdb三个软件，以及Vscode
- linux如没有gcc、make、gdb使用apt工具直接安装
- 在macos下安装了xcode的话默认已经有make和gcc，gcc是clang链接出来的，可以正常使用
- macos使用gdb使用brew工具安装
- 由于gdb在macos中安装，需要权限较高，可以使用自带的lldb代替

``` bash
$ brew install gdb
```

2. 在官方Github中克隆或者下载[lv_sim_vscode_sdl](https://github.com/lvgl/lv_sim_vscode_sdl)包

![lv_sim_vscode_sdl](https://cdn.jsdelivr.net/gh/fzxhub/image_bed@main/lvgl/lvgl77.jpeg)
3. 由于lv_sim_vscode_sdl需要的lv_drivers、lv_examples、lvgl是链接的方式；在lv_sim_vscode_sdl没有实际内容，因此，我们克隆或者下载[lv_drivers](https://github.com/lvgl/lv_drivers/tree/f14e31612409fc9216892cb58eb9d851667f8a11)、[lv_examples](https://github.com/lvgl/lv_demos/tree/4d6f215c2bfd534eda744db512ea30685e5faf75)、[lvgl](https://github.com/lvgl/lvgl/tree/c597d257984e2cd3a1c883dc97a26d4512b5e60a)

![lv_drivers](https://cdn.jsdelivr.net/gh/fzxhub/image_bed@main/lvgl/lvgl78.jpeg)

![lv_examples](https://cdn.jsdelivr.net/gh/fzxhub/image_bed@main/lvgl/lvgl79.jpeg)

![lvgl](https://cdn.jsdelivr.net/gh/fzxhub/image_bed@main/lvgl/lvgl80.jpeg)

4. 在Vscode中打开文件夹lv_sim_vscode_sdl
5. 如果是在macos使用lldb工具则在launch.json修改"MIMode"为"lldb"

``` json
{
    "version": "0.2.0",
    "configurations": [
      {
        "name": "g++ build and debug active file",
        "type": "cppdbg",
        "request": "launch",
        "program": "${workspaceFolder}/build/bin/demo",
        "args": [],
        "stopAtEntry": false,
        "cwd": "${workspaceFolder}",
        "environment": [],
        "externalConsole": false,
        "MIMode": "lldb",
        "setupCommands": [
          {
            "description": "Enable pretty-printing for gdb",
            "text": "-enable-pretty-printing",
            "ignoreFailures": true
          }
        ],
        "preLaunchTask": "Build"
      }
    ]
}
```

6. 按键F5则可以预览模拟器，模拟为官方实例程序，如需模拟自己的程序，根据官方手册替换为自己的代码即可模拟。
