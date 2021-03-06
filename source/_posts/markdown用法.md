

# 一级标题

## 二级标题

### 三级标题

#### 四级标题

##### 五级标题

###### 六级标题

```
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
```



## 字体

*斜体文本*   _斜体文本_

**粗体文本**     __粗体文本__

***粗斜体文本***    ___粗斜体文本___

```
*斜体文本*
_斜体文本_
**粗体文本**
__粗体文本__
***粗斜体文本***
___粗斜体文本___
```



## 分割线

***

******

---

------

```
***
*****
- - -
----------
```



## 删除线

~~BAIDU.COM~~

```
~~BAIDU.COM~~
```



## 下划线

下划线可以通过 HTML 的 `<u>` 标签来实现：

<u>带下划线文本</u>

```
<u>带下划线文本</u>
```



## 脚注

脚注是对文本的补充说明。

Markdown 脚注的格式如下:

创建脚注格式类似这样 [^把鼠标放上来]。

[^把鼠标放上来]: 这里是注释

```
创建脚注格式类似这样 [^把鼠标放上来]。

[^把鼠标放上来]: 这里是注释
```



## 列表

Markdown 支持有序列表和无序列表。

无序列表使用星号(*****)、加号(**+**)或是减号(**-**)作为列表标记：

* 第一项
* 第二项
* 第三项

+ 第一项
+ 第二项
+ 第三项

- 第一项
- 第二项
- 第三项

```
* 第一项
* 第二项
* 第三项

+ 第一项
+ 第二项
+ 第三项

- 第一项
- 第二项
- 第三项
```

有序列表使用数字并加上 **.** 号来表示，如：

1. 第一项
2. 第二项
3. 第三项

```
1. 第一项
2. 第二项
3. 第三项
```

列表嵌套只需在子列表中的选项添加四个空格即可：

1. 第一项：
    - 第一项嵌套的第一个元素
    - 第一项嵌套的第二个元素
2. 第二项：
    - 第二项嵌套的第一个元素
    - 第二项嵌套的第二个元素

```
1. 第一项：
    - 第一项嵌套的第一个元素
    - 第一项嵌套的第二个元素
2. 第二项：
    - 第二项嵌套的第一个元素
    - 第二项嵌套的第二个元素
```



## 区块

Markdown 区块引用是在段落开头使用 **>** 符号 ，然后后面紧跟一个**空格**符号：

> 区块引用

```
> 区块引用
```

另外区块是可以嵌套的，一个 **>** 符号是最外层，两个 **>** 符号是第一层嵌套，以此类推退：

> 最外层
> > 第一层嵌套
> >
> > > 第二层嵌套

```
> 最外层
> > 第一层嵌套
> > > 第二层嵌套
```

区块中使用列表实例如下：

> 区块中使用列表
> 1. 第一项
> 2. 第二项
> + 第一项
> + 第二项
> + 第三项

```
> 区块中使用列表
> 1. 第一项
> 2. 第二项
> + 第一项
> + 第二项
> + 第三项
```

如果要在列表项目内放进区块，那么就需要在 **>** 前添加四个空格的缩进。

区块中使用列表实例如下：

* 第一项
    > 菜鸟教程
    > 学的不仅是技术更是梦想
* 第二项

```
* 第一项
    > 菜鸟教程
    > 学的不仅是技术更是梦想
* 第二项
```



## 代码

如果是段落上的一个函数或片段的代码可以用反引号把它包起来（**`**），例如：

`printf()` 函数

```
`printf()` 函数
```

代码区块用 **```** 包裹一段代码，并指定一种语言（也可以不指定）：

```javascript
$(document).ready(function () {
    alert('RUNOOB');
});
```

```
​```javascript
$(document).ready(function () {
    alert('RUNOOB');
});
​```
```

## 链接

这是一个链接 [百度](https://www.baidu.com)

```
这是一个链接 [百度](https://www.baidu.com)
```

<https://www.runoob.com>

```
<https://www.runoob.com>
```



## 图片

Markdown 图片语法格式如下：

```
![alt 属性文本](图片地址)

![alt 属性文本](图片地址 "可选标题")
```

- 开头一个感叹号 !
- 接着一个方括号，里面放上图片的替代文字
- 接着一个普通括号，里面放上图片的网址，最后还可以用引号包住并加上选择性的 'title' 属性的文字。

使用实例：

![RUNOOB 图标](http://b-ssl.duitang.com/uploads/item/201709/02/20170902135603_2mYKC.thumb.700_0.jpeg)

![RUNOOB 图标](http://b-ssl.duitang.com/uploads/item/201709/02/20170902135603_2mYKC.thumb.700_0.jpeg "你瞅啥！")

```
![RUNOOB 图标](http://b-ssl.duitang.com/uploads/item/201709/02/20170902135603_2mYKC.thumb.700_0.jpeg)

![RUNOOB 图标](http://b-ssl.duitang.com/uploads/item/201709/02/20170902135603_2mYKC.thumb.700_0.jpeg "你瞅啥！")
```

Markdown 还没有办法指定图片的高度与宽度，如果你需要的话，你可以使用普通的 <img> 标签。

<img src="http://b-ssl.duitang.com/uploads/item/201709/02/20170902135603_2mYKC.thumb.700_0.jpeg" width="50%">

```
<img src="http://b-ssl.duitang.com/uploads/item/201709/02/20170902135603_2mYKC.thumb.700_0.jpeg" width="50%">
```



## 表格

Markdown 制作表格使用 **|** 来分隔不同的单元格，使用 **-** 来分隔表头和其他行。

语法格式如下：

| 表头   | 表头   |
| ------ | ------ |
| 单元格 | 单元格 |
| 单元格 | 单元格 |

```
|  表头   | 表头  |
|  ----  | ----  |
| 单元格  | 单元格 |
| 单元格  | 单元格 |
```

**对齐方式**

我们可以设置表格的对齐方式：

- **-:** 设置内容和标题栏居右对齐。
- **:-** 设置内容和标题栏居左对齐。
- **:-:** 设置内容和标题栏居中对齐。

| 左对齐 | 右对齐 | 居中对齐 |
| :----- | -----: | :------: |
| 单元格 | 单元格 |  单元格  |
| 单元格 | 单元格 |  单元格  |

```
| 左对齐 | 右对齐 | 居中对齐 |
| :-----| ----: | :----: |
| 单元格 | 单元格 | 单元格 |
| 单元格 | 单元格 | 单元格 |
```

## 高级技巧

不在 Markdown 涵盖范围之内的标签，都可以直接在文档里面用 HTML 撰写。

目前支持的 HTML 元素有：`<kbd> <b> <i> <em> <sup> <sub> <br> `等 ，如：

使用 <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>Del</kbd> 重启电脑

```
使用 <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>Del</kbd> 重启电脑
```

转义

Markdown 使用了很多特殊符号来表示特定的意义，如果需要显示特定的符号则需要使用转义字符，Markdown 使用反斜杠转义特殊字符：

**文本加粗** 
\*\* 正常显示星号 \*\*

```
**文本加粗** 
\*\* 正常显示星号 \*\*
```

Markdown 支持以下这些符号前面加上反斜杠来帮助插入普通的符号：

```
\   反斜线
`   反引号
*   星号
_   下划线
{}  花括号
[]  方括号
()  小括号
#   井字号
+   加号
-   减号
.   英文句点
!   感叹号
```

公式

当你需要在编辑器中插入数学公式时，可以使用两个美元符 $$ 包裹 TeX 或 LaTeX 格式的数学公式来实现。提交后，问答和文章页会根据需要加载 Mathjax 对数学公式进行渲染。如：
$$
\mathbf{V}_1 \times \mathbf{V}_2 =  \begin{vmatrix} 
\mathbf{i} & \mathbf{j} & \mathbf{k} \\
\frac{\partial X}{\partial u} &  \frac{\partial Y}{\partial u} & 0 \\
\frac{\partial X}{\partial v} &  \frac{\partial Y}{\partial v} & 0 \\
\end{vmatrix}
$$tep1}{\style{visibility:hidden}{(x+1)(x+1)}}
$$

```
$$
\mathbf{V}_1 \times \mathbf{V}_2 =  \begin{vmatrix} 
\mathbf{i} & \mathbf{j} & \mathbf{k} \\
\frac{\partial X}{\partial u} &  \frac{\partial Y}{\partial u} & 0 \\
\frac{\partial X}{\partial v} &  \frac{\partial Y}{\partial v} & 0 \\
\end{vmatrix}
$$tep1}{\style{visibility:hidden}{(x+1)(x+1)}}
$$
```