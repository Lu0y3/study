# Cmd Markdown 简明语法手册

标签： Cmd-Markdown

---

### 1. 斜体和粗体

使用 * 和 ** 表示斜体和粗体。

示例：

这是 *斜体*，这是 **粗体**。

### 2. 分级标题

使用 === 表示一级标题，使用 --- 表示二级标题。

示例：

```
这是一个一级标题
============================

这是一个二级标题
--------------------------------------------------

### 这是一个三级标题
```

你也可以选择在行首加井号表示不同级别的标题 (H1-H6)，例如：# H1, ## H2, ### H3，#### H4。

### 3. 外链接

使用 \[描述](链接地址) 为文字增加外链接。

示例：

这是去往 [本人博客](http://ghosertblog.github.com) 的链接。

### 4. 无序列表

使用 *，+，- 表示无序列表。

示例：

- 无序列表项 一
- 无序列表项 二
- 无序列表项 三

### 5. 有序列表

使用数字和点表示有序列表。

示例：

1. 有序列表项 一
2. 有序列表项 二
3. 有序列表项 三

### 6. 文字引用

使用 > 表示文字引用。

示例：

> 野火烧不尽，春风吹又生。

### 7. 行内代码块

使用 \`代码` 表示行内代码块。

示例：

让我们聊聊 `html`。

### 8.  代码块

使用 四个缩进空格 表示代码块。

示例：

    这是一个代码块，此行左侧有四个不可见的空格。

### 9.  插入图像

使用 \!\[描述](图片链接地址) 插入图像。

示例：

![我的头像](https://www.zybuluo.com/static/img/my_head.jpg)

# Cmd Markdown 高阶语法手册

### 1. 内容目录

在段落中填写 `[TOC]` 以显示全文内容的目录结构。

[TOC]

### 2. 标签分类

在编辑区任意行的列首位置输入以下代码给文稿标签：

标签： 数学 英语 Markdown

或者

Tags： 数学 英语 Markdown

### 3. 删除线

使用 ~~ 表示删除线。

~~这是一段错误的文本。~~

### 4. 注脚

使用 [^keyword] 表示注脚。

这是一个注脚[^footnote]的样例。

这是第二个注脚[^footnote2]的样例。

### 5. LaTeX 公式

$ 表示行内公式： 

质能守恒方程可以用一个很简洁的方程式 $E=mc^2$ 来表达。

$$ 表示整行公式：

$$\sum_{i=1}^n a_i=0$$

$$f(x_1,x_x,\ldots,x_n) = x_1^2 + x_2^2 + \cdots + x_n^2 $$

$$\sum^{j-1}_{k=0}{\widehat{\gamma}_{kj} z_k}$$

访问 [MathJax](http://meta.math.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference) 参考更多使用方法。

### 6. 加强的代码块

支持四十一种编程语言的语法高亮的显示，行号显示。

非代码示例：

```
$ sudo apt-get install vim-gnome
```

Python 示例：

```python
@requires_authorization
def somefunc(param1='', param2=0):
    '''A docstring'''
    if param1 > param2: # interesting
        print 'Greater'
    return (param2 - param1 + 1) or None

class SomeClass:
    pass

>>> message = '''interpreter
... prompt'''
```

JavaScript 示例：

``` javascript
/**
* nth element in the fibonacci series.
* @param n >= 0
* @return the nth element, >= 0.
*/
function fib(n) {
  var a = 1, b = 1;
  var tmp;
  while (--n >= 0) {
    tmp = a;
    a += b;
    b = tmp;
  }
  return a;
}

document.write(fib(10));
```

### 7. 流程图

#### 示例

    ```flow
    st=>start: Start:>https://www.zybuluo.com
    io=>inputoutput: verification
    op=>operation: Your Operation
    cond=>condition: Yes or No?
    sub=>subroutine: Your Subroutine
    e=>end
    st->io->op->cond
    cond(yes)->e
    cond(no)->sub->io
    ```

```flow
st=>start: Start:>https://www.zybuluo.com
io=>inputoutput: verification
op=>operation: Your Operation
cond=>condition: Yes or No?
sub=>subroutine: Your Subroutine
e=>end

st->io->op->cond
cond(yes)->e
cond(no)->sub->io
```

#### 更多语法参考：[流程图语法参考](http://adrai.github.io/flowchart.js/)

### 8. 序列图

    ```seq
    Alice->Bob: Hello Bob, how are you?
    Note right of Bob: Bob thinks
    Bob-->Alice: I am good thanks!
    ```

```seq
Alice->Bob: Hello Bob, how are you?
Note right of Bob: Bob thinks
Bob-->Alice: I am good thanks!
```

#### 更多语法参考：[序列图语法参考](http://bramp.github.io/js-sequence-diagrams/)

### 9. 甘特图

甘特图内在思想简单。基本是一条线条图，横轴表示时间，纵轴表示活动（项目），线条表示在整个期间上计划和实际的活动完成情况。它直观地表明任务计划在什么时候进行，及实际进展与计划要求的对比。

    ```mermaid
    gantt
        title 项目开发流程
        section 项目确定
            需求分析       :a1, 2024-06-22, 3d
            可行性报告     :after a1, 5d
            概念验证       : 5d
        section 项目实施
            概要设计      :2024-07-05  , 5d
            详细设计      :2024-07-08, 10d
            编码          :2024-07-15, 10d
            测试          :2024-07-22, 5d
        section 发布验收
            发布: 2d
            验收: 3d
    ```

```mermaid
gantt
    title 项目开发流程
    section 项目确定
        需求分析       :a1, 2024-06-22, 3d
        可行性报告     :after a1, 5d
        概念验证       : 5d
    section 项目实施
        概要设计      :2024-07-05  , 5d
        详细设计      :2024-07-08, 10d
        编码          :2024-07-15, 10d
        测试          :2024-07-22, 5d
    section 发布验收
        发布: 2d
        验收: 3d
```

#### 更多语法参考：[甘特图语法参考](https://mermaid.js.org/syntax/gantt.html)

### 10. 思维导图

思维导图是一种将信息以层次结构直观地组织起来的图表，显示整体各部分之间的关​​系。它通常围绕一个概念创建，在空白页的中心绘制为图像，并在其中添加相关的想法表示，例如图像、单词和单词的部分。主要思想直接与中心概念相关，其他思想从这些主要思想中分支出来。

    ```mermaid
    mindmap
      记录笔记
        准备工作
          工具选择
            纸质笔记本
            数字工具
          环境设置
            安静的地方
            良好的照明
        记录方法
          线性笔记
          思维导图
          康奈尔笔记法
        组织与整理
          分类
            主题分类
            时间分类
          复习与总结
            定期复习
            总结要点
        提高效率
          使用缩写
          高亮重点
          图表与图示
    ```

```mermaid
mindmap
  记录笔记
    准备工作
      工具选择
        纸质笔记本
        数字工具
      环境设置
        安静的地方
        良好的照明
    记录方法
      线性笔记
      思维导图
      康奈尔笔记法
    组织与整理
      分类
        主题分类
        时间分类
      复习与总结
        定期复习
        总结要点
    提高效率
      使用缩写
      高亮重点
      图表与图示
```

#### 更多语法参考：[思维导图语法参考](https://mermaid.js.org/syntax/mindmap.html)

### 11. 饼图

饼图（或圆形图）是一种圆形统计图形，被分成多个部分来表示数字比例。在饼图中，每个切片的弧长（以及其中心角和面积）与其所代表的数量成正比。虽然它因与切成薄片的饼相似而得名，但它的呈现方式却各不相同。最早的饼图通常归功于威廉·普莱费尔 1801 年的《统计简表》

    ```mermaid
    pie title 志愿者宠物领养
        "狗" : 386
        "猫" : 85
        "仓鼠" : 15
    ```

```mermaid
pie title 志愿者宠物领养
    "狗" : 386
    "猫" : 85
    "仓鼠" : 15
```

#### 更多语法参考：[饼图语法参考](https://mermaid.js.org/syntax/pie.html)

### 12. [Cmd Markdown 支持的全部十九种图表](https://www.zybuluo.com/ghosert/note/2560850)

    流程图
    序列图
    类图
    状态图
    实体关系图
    用户旅程图
    甘特图
    饼图
    象限图
    需求图
    Git图
    C4图
    思维导图
    时间线图
    桑基图
    XY图表
    框图
    包裹图
    架构图
    
#### 更多图表参考: [全部十九种图表参考](https://www.zybuluo.com/ghosert/note/2560850)

### 13. 表格支持

| 项目        | 价格   |  数量  |
| --------   | -----:  | :----:  |
| 计算机     | \$1600 |   5     |
| 手机        |   \$12   |   12   |
| 管线        |    \$1    |  234  |


### 14. 定义型列表

名词 1
:   定义 1（左侧有一个可见的冒号和四个不可见的空格）

代码块 2
:   这是代码块的定义（左侧有一个可见的冒号和四个不可见的空格）

        代码块（左侧有八个不可见的空格）

### 15. Html 标签

本站支持在 Markdown 语法中嵌套 Html 标签，譬如，你可以用 Html 写一个纵跨两行的表格：

    <table>
        <tr>
            <th rowspan="2">值班人员</th>
            <th>星期一</th>
            <th>星期二</th>
            <th>星期三</th>
        </tr>
        <tr>
            <td>李强</td>
            <td>张明</td>
            <td>王平</td>
        </tr>
    </table>


<table>
    <tr>
        <th rowspan="2">值班人员</th>
        <th>星期一</th>
        <th>星期二</th>
        <th>星期三</th>
    </tr>
    <tr>
        <td>李强</td>
        <td>张明</td>
        <td>王平</td>
    </tr>
</table>

### 16. 内嵌图标

本站的图标系统对外开放，在文档中输入

    <i class="icon-weibo"></i>

即显示微博的图标： <i class="icon-weibo icon-2x"></i>

替换 上述 `i 标签` 内的 `icon-weibo` 以显示不同的图标，例如：

    <i class="icon-renren"></i>

即显示人人的图标： <i class="icon-renren icon-2x"></i>

更多的图标和玩法可以参看 [font-awesome](https://fontawesome.com/v3/icons/) 官方网站。

### 17. 待办事宜 Todo 列表

使用带有 [ ] 或 [x] （未完成或已完成）项的列表语法撰写一个待办事宜列表，并且支持子列表嵌套以及混用Markdown语法，例如：

    - [ ] **Cmd Markdown 开发**
        - [ ] 改进 Cmd 渲染算法，使用局部渲染技术提高渲染效率
        - [ ] 支持以 PDF 格式导出文稿
        - [x] 新增Todo列表功能 [语法参考](https://github.com/blog/1375-task-lists-in-gfm-issues-pulls-comments)
        - [x] 改进 LaTex 功能
            - [x] 修复 LaTex 公式渲染问题
            - [x] 新增 LaTex 公式编号功能 [语法参考](http://docs.mathjax.org/en/latest/tex.html#tex-eq-numbers)
    - [ ] **七月旅行准备**
        - [ ] 准备邮轮上需要携带的物品
        - [ ] 浏览日本免税店的物品
        - [x] 购买蓝宝石公主号七月一日的船票
        
对应显示如下待办事宜 Todo 列表：
        
- [ ] **Cmd Markdown 开发**
    - [ ] 改进 Cmd 渲染算法，使用局部渲染技术提高渲染效率
    - [ ] 支持以 PDF 格式导出文稿
    - [x] 新增Todo列表功能 [语法参考](https://github.com/blog/1375-task-lists-in-gfm-issues-pulls-comments)
    - [x] 改进 LaTex 功能
        - [x] 修复 LaTex 公式渲染问题
        - [x] 新增 LaTex 公式编号功能 [语法参考](http://docs.mathjax.org/en/latest/tex.html#tex-eq-numbers)
- [ ] **七月旅行准备**
    - [ ] 准备邮轮上需要携带的物品
    - [ ] 浏览日本免税店的物品
    - [x] 购买蓝宝石公主号七月一日的船票
        
        
[^footnote]: 这是一个 *注脚* 的 **文本**。

[^footnote2]: 这是另一个 *注脚* 的 **文本**。


