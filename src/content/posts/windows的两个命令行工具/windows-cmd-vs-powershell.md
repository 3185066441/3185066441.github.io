---
title: Windows 为什么同时有 CMD 和 PowerShell？
published: 2026-11-15
description: 从命令、管道和脚本三个方面理解 CMD 与 PowerShell 的区别。
category: 技术笔记
tags: [Windows, 命令行, PowerShell]
---

视频作者是技术爬爬虾。笔记按原视频的五个章节整理，命令示例用于动手验证。 [B 站原视频](https://www.bilibili.com/video/BV1Nx4y147n3/) · [作者发布的 YouTube 同版](https://www.youtube.com/watch?v=u0yKHP0onwU)

## 00:00 · 为什么 Windows 有两套命令行？

CMD 和 PowerShell 都是 **Shell**，负责解释你输入的命令，也能执行脚本。CMD（`cmd.exe`）较早内置于 Windows，保留它可以继续运行既有的批处理脚本。PowerShell 后来加入，提供了更丰富的脚本语言和系统管理功能，适合处理复杂的自动化任务。 [Microsoft Learn · Windows 命令](https://learn.microsoft.com/zh-cn/windows-server/administration/windows-commands/windows-commands)

| 对比项 | CMD | PowerShell |
| --- | --- | --- |
| 常见命令 | `dir`、`cd`、`copy` | `Get-ChildItem`、`Set-Location`、`Copy-Item` |
| 管道传递的数据 | 命令的标准输出，日常用法多为文本 | Cmdlet 之间可以传递 .NET 对象 |
| 脚本扩展名 | `.bat`、`.cmd` | `.ps1` |
| 典型场景 | 运行旧批处理脚本、执行简单命令 | 筛选结构化数据、编写管理和自动化脚本 |

## 01:40 · Cmdlet 与外部程序

CMD 既有 `dir` 这样的内置命令，也能运行 `ipconfig.exe` 这样的外部程序。PowerShell 同样能运行外部程序，还提供了专为 PowerShell 设计的命令 **Cmdlet**。Cmdlet 通常采用 `动词-名词` 的形式，例如 `Get-Process` 获取进程，`Get-ChildItem` 列出目录内容。 [Microsoft Learn · 在 Shell 中运行命令](https://learn.microsoft.com/zh-cn/powershell/scripting/learn/shell/running-commands)

## 04:20 · 管道传递文本还是对象？

两个 Shell 都支持管道符 `|`，它把上一条命令的输出交给下一条命令。下面用「查找名字包含 `report` 的文件」来对照两种写法。 [Microsoft Learn · PowerShell 管道](https://learn.microsoft.com/zh-cn/powershell/module/microsoft.powershell.core/about/about_pipelines)

**CMD** 用 `dir /b /a-d` 生成文件名列表，再用 `findstr` 筛选文本行。

```bat
dir /b /a-d | findstr /i "report"
```

**PowerShell** 用 `Get-ChildItem -File -Force` 生成文件对象，包含隐藏文件。`Where-Object` 读取每个对象的 `Name` 属性来筛选，`Select-Object` 再选出文件名和字节数。

```powershell
Get-ChildItem -File -Force |
    Where-Object { $_.Name -like '*report*' } |
    Select-Object Name, Length
```

`$_` 表示管道当前处理的对象。对象还带有 `LastWriteTime` 等属性，可以直接据此筛选或排序。PowerShell 中调用的外部程序，例如 `ipconfig.exe`，常见输出仍然是文本。

## 05:45 · 脚本编程

两者都可以把多条命令写进一个脚本反复执行。已有的 `.bat` 或 `.cmd` 脚本继续交给 CMD。编写新的自动化任务时，如果需要分支、循环、函数、错误处理，或读写 CSV、JSON 等结构化数据，PowerShell 的 `.ps1` 脚本更容易组织这些操作。 [Microsoft Learn · 什么是 PowerShell](https://learn.microsoft.com/zh-cn/powershell/scripting/overview)

## 06:47 · Cmdlet 补充与命令查询

同一个名字在两个 Shell 里可能调用不同的命令。比如 `dir` 在 CMD 中是内置命令，在 Windows 上的 PowerShell 中是 `Get-ChildItem` 的别名，因此参数写法也可能不同。 [Microsoft Learn · PowerShell 别名](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_aliases)

```powershell
Get-Command dir                 # 查看 dir 在当前会话里解析成什么
Get-Command -Verb Get           # 查找以 Get 为动词的命令
Get-Help Get-ChildItem -Examples # 查看使用示例
```

CMD 中可以用 `dir /?` 查看 `dir` 的参数。复制教程命令时，先确认教程用的是哪个 Shell，再按对应语法执行。
