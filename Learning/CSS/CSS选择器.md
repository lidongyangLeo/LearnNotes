

## CSS 学习 选择器

### 语法

CSS规则有两部分构成

- 选择器

- 声明 (每个属性都有一个值，属性和值被冒号分开)

  - 属性（property）
  - 值(style attribute) 

  ```css
  p {
  	color:red;
  	text-align:center;
  }
  ```

  

###  Id 选择器和Class 选择器 

如果你要在HTML元素中设置CSS样式，你需要在元素中设置`id`和 `class`选择器。

#### id选择器

id选择器可以为标有特定id的HTML元素指定特定的样式。

HTML元素以id属性来设置id选择器，CSS中id选择器以`#`来定义。

```css
#para1 {
 tetx-align:center;
 color: red;
}
```

**id属性不要以数字开头，数字开头的ID在 Mozilla/Firebox浏览器中不起作用**。

#### class选择器

class选择器用于描述一组元素的样式，class选择器有别于id选择器，class可以在多个元素中使用。

class选择器在HTML中以class属性表示，在CSS中，类选择器以一个点`.`号显示；

```css
.center {
	text-align:center;
}
```

**类名的第一个字符不能使用数字！它无法在Mozilla或Firefox中起作用**



#### id选择器和class选择器总结

- 优先级
  - id和class同时设定的话，id的优先级高于class 
- id只能使用一个（唯一性），class可以多次使用