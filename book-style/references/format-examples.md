# 格式示例

以下示例展示新建链接时的默认格式。实际编辑时替换章节号、编号及路径，并优先兼容文档已有锚点。除明确标注的配套示例外，各代码块彼此独立，不应直接拼接成一个章节。

## 标题的单向链接

目标文件 `C02.md` 中的标题与同文件引用：

```markdown
# <span id="c02-chapter">第二章 基本方法</span>

本章先介绍[基本概念](#c02-sec-2.1)。

## <span id="c02-sec-2.1">2.1 基本概念</span>

本节正文。
```

在其他章节或 `menu.md` 中引用上述标题：

```markdown
- [第二章 基本方法](C02.md#c02-chapter)
- [第 2.1 节 基本概念](C02.md#c02-sec-2.1)
```

这两个代码块配套展示跨文件引用。标题只提供目标锚点，不添加返回链接；多个引用可以共享同一目标。

## 图与多处引用

```markdown
参见 [<span id="R_c01-fig-0001">图 1.1</span>](#c01-fig-0001)。

![不同年龄的工资分布](images/1_1.png)

[<strong><span id="c01-fig-0001">图 1.1</span></strong>](#R_c01-fig-0001) *工资与年龄的关系。* 左：*原始观测。* 右：*平均趋势。* [返回 2](#R_c01-fig-0001-2)

再次参见 [<span id="R_c01-fig-0001-2">图 1.1</span>](#c01-fig-0001)。
```

图片替代文本依据图片已知内容填写，不臆测图片细节。单图省略子图标签。没有正文引用时，图题仅写为 `<strong><span id="c01-fig-0001">图 1.1</span></strong> *说明。*`。

## HTML 表格与重复表注

```markdown
参见 [<span id="R_c05-tbl-0001">表 5.1</span>](#c05-tbl-0001)。

<table>
<thead>
<tr><th>品种</th><th>数值<a href="#c05-note-0001"><sup><span id="R_c05-note-0001">†</span></sup></a></th></tr>
</thead>
<tbody>
<tr><td>甲</td><td>2</td></tr>
<tr><td>乙</td><td>3<a href="#c05-note-0001"><sup><span id="R_c05-note-0001-2">†</span></sup></a></td></tr>
</tbody>
</table>

[<strong><span id="c05-tbl-0001">表 5.1</span></strong>](#R_c05-tbl-0001) *示例数值。*

<span id="c05-note-0001"><sup>†</sup></span> 数值为近似值。[返回 1](#R_c05-note-0001) · [返回 2](#R_c05-note-0001-2)
```

表注与章末注释共用 `note` 命名时，序号必须在本章中唯一，不能分别从同一个锚点编号开始。显示的注释符号保持原样；HTML 中的星号可写为 `<sup>*</sup>`，Markdown 普通文本中的字面星号按需转义为 `\*`。

## 章末注释

```markdown
矩阵可表示为二维数组。[<sup><span id="R_c02-note-0001">1</span></sup>](#c02-note-0001)

## 注释

<span id="c02-note-0001">1</span> 本章示例使用 `np.array()` 创建数组。[返回](#R_c02-note-0001)
```

## 编号公式

```markdown
响应与预测变量的关系可表示为：

[<span id="c02-formula-2.1">公式 2.1</span>](#R_c02-formula-2.1)

$$
Y = f(X) + \epsilon. \tag{2.1}
$$

根据公式 [<span id="R_c02-formula-2.1">(2.1)</span>](#c02-formula-2.1) 生成观测数据。
```

## 嵌套习题与代码

````markdown
3. 比较两种方法。

   - (a) 哪个答案正确？

     - i. 第一种情况。
     - ii. 第二种情况。

   - (b) 解释以下代码的输出。

     ```python
     print('fit a model with', 11, 'variables')
     ```

10. 说明第二个问题。

    - (a) 子项与该题正文的起始列对齐。
````
