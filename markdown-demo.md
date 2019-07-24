# 使用Markdown进行快速笔记

# 1、标题
# 这是一级标题
## 这是二级标题
### 这是三级标题

# 2、引用
引用符号
> 这是引用的内容
>> 这是引用的内容

# 3、分割线
---

# 4、图片（CTRL+G）
![描述](https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png)

# 5、超链接（CTRL+L）
[这是百度的超链接](https://www.baidu.com/)

# 6、列表
## 无序列表（CTRL+U）
- winter is coming
- what is dead may never die
- growing strong

## 有序列表（CTRL+SHIFT+O）
1. winter is coming
2. what is dead may never die
3. growing strong

## 7、表格
表头|表头|表头
---|:--:|---:
内容|内容|内容
内容|内容|内容

| Syntax      | Description | Test Text     |
| :---        |    :----:   |          ---: |
| Header      | Title       | Here's this   |
| Paragraph   | Text        | And more      |

姓名|技能|排行
--|:--:|--:
刘备|哭|大哥
关羽|打|二哥
张飞|骂|三弟

[markdown表格生成器](https://www.tablesgenerator.com/markdown_tables#)
[表格调整技巧](http://moxfive.xyz/2016/03/04/markdown-table-style/)

## 8、代码（CTRL+K）
- 注意这里的是键盘上1前面那个键（反引号），不是单引号


```
	function fun(){
	     echo "这是一句非常牛逼的代码";
	}
	fun();
```

```
def list_all_files(rootdir):    
    import os
    _files = []
    list = os.listdir(rootdir) #列出文件夹下所有的目录与文件
    for i in range(0,len(list)):
        path = os.path.join(rootdir,list[i])        
        if os.path.isdir(path):
            _files.extend(list_all_files(path))
        if os.path.isfile(path):
            _files.append(path)
    return _files
```

---

## 9、公式
- 公式可由MathJax渲染，由于Markdown和MathJax之间有部分转义字符冲突，所以不能和Latex完美兼容，不过绝大多数地方时一致的，要正常显示公式的话，需要做一些[配置](https://bwaycer.github.io/hugo_tutorial.hugo/tutorials/mathjax/)：

```
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
  tex2jax: {
    inlineMath: [['$','$'], ['\\(','\\)']],
    displayMath: [['$$','$$'], ['\[','\]']],
    processEscapes: true,
    processEnvironments: true,
    skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
    TeX: { equationNumbers: { autoNumber: "AMS" },
         extensions: ["AMSmath.js", "AMSsymbols.js"] }
  }
});
</script>

<script type="text/x-mathjax-config">
  MathJax.Hub.Queue(function() {
    // Fix <code> tags after MathJax finishes running. This is a
    // hack to overcome a shortcoming of Markdown. Discussion at
    // https://github.com/mojombo/jekyll/issues/199
    var all = MathJax.Hub.getAllJax(), i;
    for(i = 0; i < all.length; i += 1) {
        all[i].SourceElement().parentNode.className += ' has-jax';
    }
});
</script>

<script type="text/javascript"
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>
```

- 配置完成之后，大部分的工时都可以正常显示（**Tools-->Option-->Markdown**-->Markdown processor选Github Flavored Markdown）：


$$x_{1,2} = {-b\pm\sqrt{b^2 - 4ac} \over 2a}.$$ 

$$|\vec{A}|=\sqrt{A_{x1}^2 + A_{y1}^2 + A_z^2}.$$

###公式中存在的问题
当输入如下内容时：
```
$$T^{\mu\nu}=\begin{pmatrix}
\varepsilon&0&0&0\\
0&\varepsilon/3&0&0\\
0&0&\varepsilon/3&0\\
0&0&0&\varepsilon/3
\end{pmatrix},$$
```
显示结果为
$$T^{\mu\nu}=\begin{pmatrix}
\varepsilon&0&0&0\\
0&\varepsilon/3&0&0\\
0&0&\varepsilon/3&0\\
0&0&0&\varepsilon/3
\end{pmatrix},$$

这并不是我们希望看到的，我们需要显示的结果如下：
$$T^{\mu\nu}=\begin{pmatrix}
\varepsilon&0&0&0\\\\
0&\varepsilon/3&0&0\\\\
0&0&\varepsilon/3&0\\\\
0&0&0&\varepsilon/3
\end{pmatrix},$$

> 操作方法：把`\\`换成`\\\\`


# 10、生成目录
```
<script>
    document.addEventListener("DOMContentLoaded", function() {
        // 生成目录列表
        var outline = document.createElement("ul");
        outline.setAttribute("id", "outline-list");
        outline.style.cssText = "border: 1px solid #ccc;";
        document.body.insertBefore(outline, document.body.childNodes[0]);
        // 获取所有标题
        var headers = document.querySelectorAll('h1,h2,h3,h4,h5,h6');
        for (var i = 0; i < headers.length; i++) {
            var header = headers[i];
            var hash = _hashCode(header.textContent);
            // MarkdownPad2无法为中文header正确生成id，这里生成一个
            header.setAttribute("id", header.tagName + hash);
            // 找出它是H几，为后面前置空格准备
            var prefix = parseInt(header.tagName.replace('H', ''), 10);
            outline.appendChild(document.createElement("li"));
            var a = document.createElement("a");
            // 为目录项设置链接
            a.setAttribute("href", "#" + header.tagName + hash)
            // 目录项文本前面放置对应的空格
            a.innerHTML = new Array(prefix * 4).join('&nbsp;') + header.textContent;
            outline.lastChild.appendChild(a);
        }
    });
    // 类似Java的hash生成方式，为一段文字生成一段基本不会重复的数字
    function _hashCode(txt) {
         var hash = 0;
         if (txt.length == 0) return hash;
         for (i = 0; i < txt.length; i++) {
              char = txt.charCodeAt(i);
              hash = ((hash<<5)-hash)+char;
              hash = hash & hash; // Convert to 32bit integer
         }
         return hash;
    }
</script>
```







