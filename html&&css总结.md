​
--本人才疏学浅，如有错漏之处欢迎指正
目录
目录

我们先从前端DOM api的角度审视以下Html和css,它提供了一种从编程视角认知HTML和CSS的有效视图。

对于CSS，我们主要讨论它的盒子模型。

而对于HTML，表单和列表自然是不可不谈的。

前端浏览器以DOM树的方式展开HTML文档。

这是一种“结构化”，或者说是“层次的”,也是HTML与txt文件的本质性差别。

任何具有实际功能的web界面都需要与编程语言相连接（通常是JS）,而DOM对编程语言提供了有关文件必要的编程接口，使得程序员可以去操控界面。有人给出过一个有趣的等式：API (web 或 XML 页面) = DOM + JS (脚本语言)

DOM树结构中包括：
1.一个文档节点，即文档本身

2.HTML元素节点，就是HTML标签

3.HTML文本节点，标签内部的文字信息

4.HTML属性节点，用来设定标签元素的具体信息。一般来说，如果程序员没有指定相关的属性内容，浏览器会用自己的默认方式展示。

编程语言最常见的增删改查操作对于DOM树节点都是可行的。

一般来讲程序员在选择编写HTML页面时对标签的使用具有很大的灵活性，但是如<DOCTYPE html>,<head>,<body>标签被认为是必要的。

CSSOM（CSS对象模型）
就是与DOM很近似的概念。模仿这种方式这就很自然地得到了CSS中选择器的思想：根据指定特征选定元素。
虽然结构类似，但是只有HTML DOM才具有完整的树形结构关系。在计算机中，DOM承担了语义职能，而CSSOM承担了表现职能。

CSSOM又可以进一步分解为负责样式表和规则的model以及被称为view的视图api。

而CSS本身的核心思想可以用层叠,继承和权重来概括。

层叠最直接的使用就是z-index属性，它设置元素的层叠级别；

在界面中，所有的元素都具有一个层叠水平，但它并不与z-index等价。层叠上下文是可以嵌套的。

我们可以考虑在平面中有两个元素发生了（部分）重叠,这时用户可能只看到一个元素，因为实际上元素将在第三维的方向上发生堆叠。这时这些元素被称为层叠上下文元素。并且，元素只能在同一个层叠上下文中直接比较层叠等级。而不同层叠上下文之间由是父级层叠上下文层叠等级比较决定。

当存在层叠上下文时，决定元素显示的规则是层叠顺序。

层叠顺序有这样一张图：


![avatar](https://img-blog.csdnimg.cn/925dc91ee38b4bedb7ca7df30066fcc5.png)
关于CSS的通用性，理论上可以把它和任何结构化文档格式一起使用。

css通过引入文件,内部和外部的方式设置页面HTML内容的样式，它不会破坏结构，所以可以说它是“静态”的，但它在图像显示上相当自由，甚至可以设置动画。

事实上，浏览器解析CSS，会生成一个CSS规制树，CSS的解析结构会与DOM树一起构成渲染树。渲染树中的元素都能对应到DOM树上。浏览器通过DOM树计算节点在页面中位置，然后进行渲染。渲染树描述可见的DOM内容，将CSS样式信息附加到节点上。通过渲染树，浏览器进行网页的绘制以及布局。

当然，我们通过DOM可以获得页面中的对象，在JS的文章里我们再进一步讨论相关内容。

从内容上看，CSS选择器大体分为全体选择器，标签选择器，元素(在HTML中，标签之内的全部代码被称为元素)选择器和id选择器,伪类选择器。

而在数量上单个的内容称为简单选择器。在多个的情况下还可以通过使用空格连接表示复合选择器，逗号连接表示选择器列表。

CSS选择器具有优先级，id选择器>class,伪类>类型,伪元素。

CSS盒子模型
首先你的html文件应该要有定义doctype标签，否则浏览器可能用一种奇怪的方式显示盒子。

形象地说，Border圈定了纸上田字格的范围，padding则划出了田字格到纸边缘的空白内容

事实上padding是透明的，放不了东西

关于这个内容，我认为单纯的文字叙述太空泛了，所以我们结合具体代码来看：

首先我们来看一串代码及其效果 

![avatar](https://img-blog.csdnimg.cn/2a983aa7dbad443f8aa3581712ab8b8e.png)
  ![avatar](https://img-blog.csdnimg.cn/00ed4e78499241459e18b8c6ce6f46e7.png)


然后稍微更改一下

![avatar](https://img-blog.csdnimg.cn/57ff96bb821a4fba8f14b0f60a23caa6.png)

![avatar](https://img-blog.csdnimg.cn/47d164c6b5f74827bc6b65fcaf7818e3.png)

这是实际显示效果，注意字附近白框是border的边框。字的大小并没有明显改变 ，可见这是决定了浏览器会分配多少空间来放盒子里面的信息，border在随之改变，至于border里面能不能放下，会不会把内部的东西“露出来”就是无法保证的了。

![avatar](https://img-blog.csdnimg.cn/d40c7e99abfc4d7881ef0371ec3a8bb6.png)
  ![avatar](https://img-blog.csdnimg.cn/285d1dd84a7943f18590fccd142dace0.png)

稍微改下

![avatar](https://img-blog.csdnimg.cn/697ebc9ee6e64172842c75bc9173eebf.png)
  ![avatar](https://img-blog.csdnimg.cn/87ef5f44b8ee493295d26e1f1bc729c5.png)

 这里两个边框距离缩短了，那么如果两个padding都是0，并且margin是0

 
![avatar](https://img-blog.csdnimg.cn/55dbb26c0d644b168f5824013aaa4548.png)
  ![avatar](https://img-blog.csdnimg.cn/33144e9023994f60a028a8970c39a62a.png)


左右已经重叠了，但是上下还没有合并，应该是因为border_style



去掉后果然重合了 

  另外我们可以通过overflow: hidden;(我更推荐 overflow:scroll;更加智能，会在竖直和水平两个方向设置滚动条)设置边距不重合

浏览器计算结果 
![avatar](https://img-blog.csdnimg.cn/c442fd6bffd740c781fb984c0b228f7a.png)


html代码

![avatar](https://img-blog.csdnimg.cn/17f461740219496da873e9dc1ac9efdb.png)

HTML表单及列表
我们以

样式图：
![avatar](https://img-blog.csdnimg.cn/b32a7821d74143d5a78a220ee5d6bc87.png)


 相关的html代码如下：

<form name="signup" method="get">
    <ul>
        <li>
            <div class="dropdown" style="background-color:#bbe3d2e7;">
                <p>注册属于自己的新账号</p>
            </div>

        </li>
        <li>
            <label for="accountnumbers">账号:</label>
            <input type="text" id="accountnumbers" name="accountnumbers" placeholder="请输入账号">
        </li>
        <li> <label for="name">名称:</label>
        <input type="text" id="name" name="name" placeholder="名称">
        </li>
        <li>
            <label for="password0">密码:</label>
            <input type="password" id="password0" name="password" placeholder="请输入数字">
        </li>
        <li >
            <label for="tel">电话:</label>
            <input type="text" id="tel" name="tel" placeholder="设置电话">
            <p>收货地区</p>
            <select id="seleHome" >   </select>
        </li>
        <li class="button">
            <button type="submit" onclick="submitInfo();">注册</button>
        </li>
    </ul>
</form>
由于篇幅和主题的限制，与具体业务相关的一些js的函数没有包括在这里（我们只要纯的HTML）

我们看到表单中要提交的信息一般放在input文本输入框里面，或者是select标签里，作为要向后端提交的信息，最后表单一定要有一个submit按钮用于提交信息（会跳转到目的界面，也可以用js把跳转关掉）

​
