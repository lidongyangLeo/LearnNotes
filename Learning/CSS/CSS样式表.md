



## CSS 样式表

### 如何插入式样表

- 外部式样表
- 内部式样表
- 内联样式

#### 外部式样表

当样式需要应用于很多页面时，外部式样表将是理想的选择。在使用外部式样表的情况下，你可以通过改变一个文件来改变整个站点的外观。每个页面使用<link>标签链接到样式表。<link>标签在文档的头部

```html
<head>
<link rel="stylesheet" type="text/css" href="mystyle.css">
</head>
```

浏览器会从文件mystyle.css中读到样式声明，并根据它来格式文档。

外部样式表可以在任何文本编辑器中进行编辑。文件不能包含任何的html标签。样式表应该以.css扩展名进行保存

#### 内部式样表

当单个文档需要特殊的样式时，就应该使用内部样式表。你可以使用`<style>`标签在文档头部定义内部式样表。

```html
<head>
  <style>
    hr {
      color: red;
    }
    p {
      margin-left:20px;
    }
    body {
      background-image:url("image/back40.gif");
    }
  </style>
</head>
```



#### 内联式样

由于要将表现和内容混杂在一起，内联样式会损失掉样式表的许多优势。

要使用内联样式，你需要在相关的标签内使用样式（style）属性。style属性可以包含任何CSS属性。

```html
<p style="color:red;margin-left:20px">
  这是一个段落
</p>
```

#### 多重样式

如果某些属性在不用的样式表中被同样的选择器定义，那么属性值将从更具体的样式表中被继承过来。

例如：外部样式表拥有针对h3选择器的三个属性

```css
h3 {
  color: red;
  text-align:left;
  font-size:8pt;
}
```

而内部样式表拥有针对h3选择器的两个属性

```css
h3 {
  text-align:center;
  font-size:20pt;
}
```

例如拥有内部样式表的这个页面同时与外部样式表链接，那么h3得到的样式是

```css
color:red
text-align:center;
fons-size:20pt
```

即样色属性将被继承于外部样式表，而文字排列和字体尺寸会被内部样式表中的规则取代。



#### 多重样式优先级

样式表允许以多种方式规定样式信息。样式可以规定在单个的HTML元素中，在HTML页的头元素中，或在一个外部的CSS文件中。甚至可以在用一个HTML文档内部引用多个外部样式表。

内联样式（inline style） > 内部样式 Internal style sheet > 外部样式 external style sheet > 浏览器默认样式



