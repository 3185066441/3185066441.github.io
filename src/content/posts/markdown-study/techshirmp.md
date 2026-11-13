---
title: 学习Markdown基本语法
published: 2023-09-09
description: This is the first post of my study blog.
image: ./fd4aeed1-ca74-448e-b786-68fa236feee6.png

tags: [markdown, note]
category: tools
draft: false
# lang: jp      # Set only if the post's language differs from the site's language in `config.ts`
---

# ＃空格后面是标题 
## 两个＃就是二级标题

换行使用<br>br标签

代码块用三个反引号后面跟上代码类型
```python
print("hello world")
```

图片格式是感叹号 ! + [image.png](/xiangduilujing)

ctrl + shift + v可以预览

### 下面这些由gpt大人整理:

## **一、Markdown 常用语法速查表**

| 功能   | Markdown 写法               | 效果            |
| ---- | ------------------------- | ------------- |
| 一级标题 | `# 标题`                    | 最大标题          |
| 二级标题 | `## 标题`                   | 次级标题          |
| 三级标题 | `### 标题`                  | 三级标题          |
| 加粗   | `**重要内容**`                | **重要内容**      |
| 斜体   | `*文字*`                    | *文字*          |
| 删除线  | `~~文字~~`                  | ~~文字~~        |
| 行内代码 | `` `print("Hi")` ``       | `print("Hi")` |
| 无序列表 | `- 内容`                    | 圆点列表          |
| 有序列表 | `1. 内容`                   | 数字列表          |
| 任务列表 | `- [ ] 任务`                | 复选框           |
| 引用   | `> 内容`                    | 引用块           |
| 分割线  | `---`                     | 水平分割线         |
| 超链接  | `[百度](https://baidu.com)` | 可点击链接         |
| 图片   | `![描述](image.png)`        | 插入图片          |
| 换行   | 行末加两个空格或 `<br>`           | 强制换行          |

## **二、重点补充的语法**

### **1. 列表（非常常用）**

Markdown 源码

```

- Python
- C++
- Java

1. 安装 Python
2. 安装 VS Code
3. 运行程序

```

渲染效果

- Python
- C++
- Java

1. 安装 Python
2. 安装 VS Code
3. 运行程序

### **2. 任务列表（GitHub 很常见）**

```

- [x] 学习 Python
- [x] 学习 Markdown
- [ ] 学习 Docker
- [ ] 完成项目

```

效果如下：

- [x] 学习 Python
- [x] 学习 Markdown
- [ ] 学习 Docker
- [ ] 完成项目

### **3. 超链接（重点区分图片）**

```

[GitHub官网](https://github.com)

![我的图片](./images/example.png)

```

两者主要区别：图片语法多一个 `!`。

其中：

- 表示显示文字或图片描述。
- `()` 表示链接地址或图片路径。
- `./` 表示当前目录，`../` 表示上一级目录。

### **4. 引用**

```

> 这是一段引用
>
> 这是引用的第二段

```

效果：

> 这是一段引用
>
> 这是引用的第二段

### **5. 表格（写 README 很有用）**

```

| 模型 | 参数量 | 用途 |
|---|---|---|
| BERT | 110M | 文本理解 |
| GPT-2 | 1.5B | 文本生成 |
| ResNet-50 | 25.6M | 图像分类 |

```

效果：

| 模型        | 参数量   | 用途   |
| --------- | ----- | ---- |
| BERT      | 110M  | 文本理解 |
| GPT-2     | 1.5B  | 图像分类 |
| ResNet-50 | 25.6M | 图像分类 |

### **6. 代码块与行内代码**

你已经会三个反引号了，还需要区分两种情况。

**行内代码**：用一个反引号包裹，例如 `pip install numpy`。

**多行代码**：用三个反引号包裹，可以指定语言。

````

```python
import numpy as np

a = np.array([1, 2, 3])
print(a)
```

````

注意，你原来写的 `printf("hello world")` 是 C 语言风格，而 Python 应使用 `print("hello world")`。

### **7. 数学公式（研究生写笔记很实用）**

许多 Markdown 编辑器（例如支持数学功能的 VS Code 预览插件、Jupyter）可以用 LaTeX 语法写公式。

行内公式：

```

损失函数为 $L = (y-\hat{y})^2$

```

独立公式：

```

$$
\mathrm{Attention}(Q,K,V)
=\mathrm{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V
$$

```

效果：
$$
 \mathrm{Attention}(Q,K,V)= \mathrm{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V 
$$

注意：`$...$` 和 `$$...$$` 是常见扩展，并非所有 Markdown 渲染器默认支持。

## **三、你原来的笔记有两点需要注意**

**第一，Markdown 换行不一定需要&#x20;**`<br>`**。**

通常按一次 Enter，源码会换行，但渲染时可能仍在同一段；空一行表示新段落。需要强制换行时，可以在行末输入两个空格再按 Enter，也可以使用 `<br>`（取决于平台是否支持 HTML）。

**第二，**`Ctrl + Shift + V`**&#x20;不是所有软件通用的预览快捷键。**

在 VS Code 中，它通常是打开 Markdown 预览；`Ctrl + K` 后按 `V` 则可以在侧边打开预览。其他编辑器的快捷键可能不同。
