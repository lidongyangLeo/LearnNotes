## PX （绝对长度单位）

px 像素（Pixel） 像素px是相对于显示器屏幕分辨率而言的。

特点：

- IE 无法调整那些使用px作为单位的字体大小；
- 国外的大部分网站能够调整的原因在于其使用了em或rem作为字体单体；
- Firefox能够调整px和em,rem。但是96%以上的中国网名使用IE浏览器（或内核）

## em (相对长度单位)

em(front size of the element) 是指相对于父元素字体大小的单位。

**使用**

- 浏览器的默认字体都是16px,那么1em=16px， 以此类推计算12px=0.75, 10px=0.625em；2em=32px
- 使用很复杂，很难很好的与px进行对应，也导致书写，使用，视觉的复杂（0.75em、0.625em全是小数点）
- 为了简化font-size的换算，我们在body 中写入了一段代码

```css
body {
  font-size: 62.5%;
}
// 公式 16px * 62.5 = 10px
```

这样页面中1em=10px, 1.2em = 12px; 1.4em=14px; 1.6em=16px .使得视觉、使用、书写都得到了极大的帮助

例如：

```html
<div class="font1" style="font-size: 1.6em">我是1.6em</div>
```

缺点：

- em的值并不是固定的
- em会继承父级元素的字体大小 （参考物是父元素的font-size）
- em中所有的字体都是相对于父元素的大小决定的，所以如果一个设置了font-size：1.2em的元素，在另一个设置了font-size: 1.2em的元素里，而这个元素又在另一个元素又在另一个设置了font-size:1.2em的元素里，那么最后计算的结果是1.2* 1.2*1.2 = 1.728em

例如：

```html
<div class="big">
我是大字体
 <div class="small">我是小字体</div>
</div>
```

```html
<style>
body {
	font-size: 62.5%;
}
.big {
	font-size: 1.2em
}
.small {
	font-size: 1.2em
}
</style>
```

但运行结果small 字体大小为： 1.2em * 1.2em = 1.44em

宽**度高度也是同理**

## rem

rem和em相似，但是rem是相对于根元素的字体大小单位。与em相比，rem更方便计算也更加直观。但是rem在IE8及其以下都不兼容。

特点：

- rem 单位可谓集相对大小和绝对大小的优点于一身
- 和em不同的是rem总是相对于根元素（如：root{}）,而不像em一样使用级联的方式来计算尺寸。这种相对单位使用起来更简单。
- rem支持IE9及以上，意思是相对于根元素html(网页)，不会像em那也，依赖于父元素的字体大小，而造成混乱。使用起来安全了很多。

```html
<div class="big">
	我是14px=1.4rem<div class="small">我是12px=1.2rem</div>
</div>
```

```html
<style>
	html {font-size: 10px} /* 公式16px* 62.5% = 10x*/
	.big {
		font-size: 1.4rem
  }
	.small {
		font-size: 1.2rem
	}
</style>
```

其长度单位：

vw: 1vw等于视口宽度的1%

vh: 1vh等于视口高度的1%

vmin： 选取vw和vh中最小的那个

vmax: 选取vw和vh中最大的那个
