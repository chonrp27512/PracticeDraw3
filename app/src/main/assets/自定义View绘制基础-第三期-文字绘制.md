#自定义View绘制基础-第三期-文字绘制

![](https://user-gold-cdn.xitu.io/2017/7/24/ddefb9fc0f353522616f6f033b6b7804?imageView2/0/w/1280/h/960/ignore-error/1)


## 1. Canvas 绘制文字的方式
	
	Canvas的文字绘制方法有三个：
		1，drawText()
		2，drawTextRun()
		3，drawTextOnPath()

### 1.1drawText(String text,float x,float y,Paint paint)
	drawText()是最基本绘制文字的方法：给出文字的内容和位置，去绘制文字

	x,y是文字的坐标，要注意，这个坐标是在文字的左下角靠左一点距离的位置。
大概在这里
![](https://user-gold-cdn.xitu.io/2017/7/24/bc947a220cfddfc97d5d66b16725d56a?imageView2/0/w/1280/h/960/ignore-error/1)

![](https://user-gold-cdn.xitu.io/2017/7/24/5c7235b776712d1d95e543a243858578?imageView2/0/w/1280/h/960/ignore-error/1)

参数中的y，指的就是基线baseline，也就是下面这条线。
![](https://user-gold-cdn.xitu.io/2017/7/24/509ee839eef0404b25ee678d02f72d55?imageView2/0/w/1280/h/960/ignore-error/1)

每个字母或字之间都有一定的空隙，就像这样
![](https://user-gold-cdn.xitu.io/2017/7/24/c937c6adeb27c623554618309ad80221?imageView2/0/w/1280/h/960/ignore-error/1)

### 1.2 drawTextRun(CharSequence text,int start,int end,int contextStart,int contextEnd,float x,float y,boolean isRtl,Paint paint)
	这个对中国人没用
		1，设置上下文
		2，文字方向
	参数：
		text  要绘制的文字
		start 从哪个字开始绘制
		end   绘制到哪个字结束
		contextStart  上下文的起始位置，contextStart需要小于等于start
		contextEnd 上下文的结束位置，contextEnd需要大于等于end
		x 文字左边的坐标
		y 文字的基线坐标
		isRtl  是否是RTL（Right to Left从右向左）
如下图：
![](https://user-gold-cdn.xitu.io/2017/7/24/0e3debb0fd0edcdbf5ddea8771701624?imageView2/0/w/1280/h/960/ignore-error/1)

### 1.3 drawTextOnPath(String text,Path path,float hOffset,float vOffset,Paint paint)
	
	沿着一条线绘制文字
	text 绘制内容
	path 绘制的path路径
	hOffset 文字相对于Path的水平偏移量
	vOffset 文字相对于Path的竖直偏移量
	
	例如：
		hOffset=5，vOffset=10，那么文字就会右移5像素和下移10像素

![](https://user-gold-cdn.xitu.io/2017/7/24/4ebcf7143a781a82ad110058e9c5b2b2?imageView2/0/w/1280/h/960/ignore-error/1)


## 1.4 StaticLayout 换行绘制文字
	
	Canvas里绘制文字不能换行，也不能识别\n换行符。
	它是android.text.Layout的子类。纯粹用来绘制文字的。支持换行。也会在\n处换行。

![](https://user-gold-cdn.xitu.io/2017/7/24/bc3c0f85fb986ed3262164ac1cb07f74?imageView2/0/w/1280/h/960/ignore-error/1)	

## 2 Paint对文字绘制的辅助

	paint对文字的辅助，有两类的方法：设置显示效果的和测量文字尺寸的。
### 2.1 设置显示效果类
#### 2.1.1 setTextSize(float textsize) 设置文字的大小
![](https://user-gold-cdn.xitu.io/2017/7/24/d41956a45fe5cb6d14a2f1200e60713f?imageView2/0/w/1280/h/960/ignore-error/1)
	
	paint.setTextSize(int)
### 2.1.2 setTypeface(Typeface)
	
	paint.setTypeface(Type.DEFAULT)
![](https://user-gold-cdn.xitu.io/2017/7/24/87c38c2294746a37be9925f52bc6ad5b?imageView2/0/w/1280/h/960/ignore-error/1)
### 2.1.3 setFakeBoldText(boolean)
	是否使用伪粗体
	paint.setFakeBoldText(false)
![](https://user-gold-cdn.xitu.io/2017/7/24/22131d8a3f4ccbb4c8b97aadf3666e8a?imageView2/0/w/1280/h/960/ignore-error/1)
### 2.1.4 setStrikeThruText(boolean)
	是否加删除线
![](https://user-gold-cdn.xitu.io/2017/7/24/41591522eb91f7ecc1d6d8745f38f9cc?imageView2/0/w/1280/h/960/ignore-error/1)
### 2.1.5 setUnderlineText(boolean)
	加下划线
![](https://user-gold-cdn.xitu.io/2017/7/24/3239a9531334a481de1cbf97a26cf22f?imageView2/0/w/1280/h/960/ignore-error/1)
### 2.1.6 setTextSkewX(float)
	设置文字横向错切角度，就是倾斜度
![](https://user-gold-cdn.xitu.io/2017/7/24/176824a7ae83670900171021c45f585c?imageView2/0/w/1280/h/960/ignore-error/1)

### 2.1.7 setTextScaleX(float)
	设置文字横向放缩，变胖变瘦
![](https://user-gold-cdn.xitu.io/2017/7/24/f2dec8076bd3d4351dc4d8ca19fba9bd?imageView2/0/w/1280/h/960/ignore-error/1)
### 2.1.8 setLetterSpacing(float)
	设置字符间距，默认0
![](https://user-gold-cdn.xitu.io/2017/7/24/990d311f61aed92f372b2e31ff25af8d?imageView2/0/w/1280/h/960/ignore-error/1)
### 2.1.9 setFontFeatureSettings(String)
	用CSS的font-feature-settings的方式来设置文字
![](https://user-gold-cdn.xitu.io/2017/7/24/0ecf429806a159d3ee608e8bfbe6c726?imageView2/0/w/1280/h/960/ignore-error/1)
CSS样式查看这里：
[https://www.w3.org/TR/css-fonts-3/#font-feature-settings-prop](https://www.w3.org/TR/css-fonts-3/#font-feature-settings-prop)
### 2.1.10 setTextAlign(Paint.Align )
	文字对齐方式
		LEFT,RIGHT,CENTER
![](https://user-gold-cdn.xitu.io/2017/7/24/6fc7152c2c55019c1d8379611bfc0186?imageView2/0/w/1280/h/960/ignore-error/1)
### 2.1.11 setTextCocale(Locale) / setTextLocales(LocaleList)

	设置的语言和语言区域

	paint.setTextLocale(Locale.CHINA); // 简体中文
	canvas.drawText(text, 150, 150, paint);
	paint.setTextLocale(Locale.TAIWAN); // 繁体中文
	canvas.drawText(text, 150, 150 + textHeight, paint);
	paint.setTextLocale(Locale.JAPAN); // 日语
	canvas.drawText(text, 150, 150 + textHeight * 2, paint);
![](https://user-gold-cdn.xitu.io/2017/7/24/8b6a7e163bb19c06d4965b79b98438f2?imageView2/0/w/1280/h/960/ignore-error/1)

### 2.1.12 setHinting(int mode) 是否启动字体的hinting 字体微调

	android设置大多数都是用的矢量字体。矢量字体的原理是对每个字体给出一个字形的矢量描述，然后使用这个矢量来对所有的尺寸的字体来生成对应的字形。
	比如字体较大时，矢量字体能保持字体的圆润，这就是矢量字体的优势。
不过现在手机像素高，这个基本没啥用了。
![](https://user-gold-cdn.xitu.io/2017/7/24/a57b0b87a341772bfe75e1d845a9e69a?imageView2/0/w/1280/h/960/ignore-error/1)

### 2.1.13 setElegantTextHeight(boolean)
	这个对中国人没用。限制字的高度

### 2.1.14 setSubpixelText(boolean)
	是否开启次像素级的抗锯齿
	这个方法也就是增强的抗锯齿，不过默认的抗锯齿够好了，这个也没啥用了。
### 2.1.15 setLiearText(boolean)

## 2.2 测量文字尺寸类
### 2.2.1 float getFontSpacing()
	获取推荐的行距
	即推荐的两行文字的 baseline 的距离。这个值是系统根据文字的字体和字号自动计算的。
	它的作用是当你要手动绘制多行文字（而不是使用 StaticLayout）的时候，可以在换行的时候给 y 坐标加上这个值来下移文字。
	
	canvas.drawText(texts[0], 100, 150, paint);
	canvas.drawText(texts[1], 100, 150 + paint.getFontSpacing, paint);
	canvas.drawText(texts[2], 100, 150 + paint.getFontSpacing * 2, paint);
![](https://user-gold-cdn.xitu.io/2017/7/24/dbaab0f11ec2a84edc5cb56ea4a9646b?imageView2/0/w/1280/h/960/ignore-error/1)

### 2.2.2 FontMetrcs getFontMetrics()
	获取paint的fontMetrics
	相对专业的工具类。
	它提供了几个文字排印方面的数值。
		ascent  大部分字型不会超过这条线
		descent 大部分字形不会超过这条线
		top 所有字形不超过这条线
		bottom 所有字形不超过这条线
		leading 上行的top和下行的bottom之间的距离，小细缝 
![](https://user-gold-cdn.xitu.io/2017/7/24/ddefb9fc0f353522616f6f033b6b7804?imageView2/0/w/1280/h/960/ignore-error/1)	

### 2.2.3 getTextBounds(String text,int start,int end,Rect bounds)
	获取文字的显示范围
	text 测量的文字
	start 起始位置
	end 结束位置
	bounds 存储文字显示范围的对象
### 2.2.4 float measureText(String text)
	测量文字的宽度并返回
	getTextBounds: 它测量的是文字的显示范围（关键词：显示）。
	形象点来说，你这段文字外放置一个可变的矩形，然后把矩形尽可能地缩小，一直小到这个矩形恰好紧紧包裹住文字，那么这个矩形的范围，就是这段文字的 bounds。

	measureText(): 它测量的是文字绘制时所占用的宽度（关键词：占用）。前面已经讲过，一个文字在界面中，往往需要占用比他的实际显示宽度更多一点的宽度，以此来让文字和文字之间保留一些间距，不会显得过于拥挤。
	上面的这幅图，我并没有设置 setLetterSpacing() ，这里的 letter spacing 是默认值 0，但你可以看到，图中每两个字母之间都是有空隙的。
	另外，下方那条用于表示文字宽度的横线，在左边超出了第一个字母 H 一段距离的，在右边也超出了最后一个字母 r（虽然右边这里用肉眼不太容易分辨），而就是两边的这两个「超出」，导致了 measureText() 比 getTextBounds() 测量出的宽度要大一些。

### 2.2.5 getTextWidths(String text,float[] widths)
	获取字符串中每个字符的宽度，并把结果填入参数widths。
	这相当于measureText()的一个快捷方法。
### 2.2.6 int breakText(String text,boolean measureForwards,float maxWidth,float[] measuredWidth)
	这个方法也是用来测量文字宽度的。但是和measureText()的区别是，breakText()是在给出宽度上限的前提下测量文字的宽度。如果超过文字宽度上限，就会截断文字。
	
	int measuredCount;
	float[] measuredWidth = {0};

	// 宽度上限 300 （不够用，截断）
	measuredCount = paint.breakText(text, 0, text.length(), true, 300, measuredWidth);
	canvas.drawText(text, 0, measuredCount, 150, 150, paint);

	// 宽度上限 400 （不够用，截断）
	measuredCount = paint.breakText(text, 0, text.length(), true, 400, measuredWidth);
	canvas.drawText(text, 0, measuredCount, 150, 150 + fontSpacing, paint);
	
	// 宽度上限 500 （够用）
	measuredCount = paint.breakText(text, 0, text.length(), true, 500, measuredWidth);
	canvas.drawText(text, 0, measuredCount, 150, 150 + fontSpacing * 2, paint);
	
	// 宽度上限 600 （够用）
	measuredCount = paint.breakText(text, 0, text.length(), true, 600, measuredWidth);
	canvas.drawText(text, 0, measuredCount, 150, 150 + fontSpacing * 3, paint);
![](https://user-gold-cdn.xitu.io/2017/7/24/2c0a8940aa3e18725840062ff138269d?imageView2/0/w/1280/h/960/ignore-error/1)
	
	breakText() 的返回值是截取的文字个数（如果宽度没有超限，则是文字的总个数）。
	参数中， 
	text 是要测量的文字；
	measureForwards 表示文字的测量方向，true 表示由左往右测量；
	maxWidth 是给出的宽度上限；
	measuredWidth 是用于接受数据，而不是用于提供数据的：方法测量完成后会把截取的文字宽度（如果宽度没有超限，则为文字总宽度）赋值给 measuredWidth[0]。
### 2.2.7 光标相关
	对于EditText以及类似的场景，会需要绘制光标。光标的计算很麻烦，不过API23引入了两个新的方法，有了这两个方法后，计算光标就方便多了。
	
#### 2.2.7.1 getRunAdvance(CharSequence text,int start,int end,int contextStart,int contextEnd,boolean isRtl,int offset)
	text 绘制文字的内容
	start end 文字的起始位置和结束位置
	contextStart contextEnd 上下文的起始和结束坐标
	isTrl 文字的方向
	offset 字数的便宜 计算第几个字符处的光标
	
	int length = text.length();
	float advance = paint.getRunAdvance(text, 0, length, 0, length, false, length);
	canvas.drawText(text, offsetX, offsetY, paint);
	canvas.drawLine(offsetX + advance, offsetY - 50, offsetX + advance, offsetY + 10, paint);
![](https://user-gold-cdn.xitu.io/2017/7/24/b4dbafaba8b1fb6c92a73bade3f2d3de?imageView2/0/w/1280/h/960/ignore-error/1)
	getRunAdvance()能做的事比measureText()多了
	
	// 包含特殊符号的绘制（如 emoji 表情）
	String text = "Hello HenCoder \uD83C\uDDE8\uD83C\uDDF3" // "Hello HenCoder 🇨🇳"
	
	...
	
	float advance1 = paint.getRunAdvance(text, 0, length, 0, length, false, length);
	float advance2 = paint.getRunAdvance(text, 0, length, 0, length, false, length - 1);
	float advance3 = paint.getRunAdvance(text, 0, length, 0, length, false, length - 2);
	float advance4 = paint.getRunAdvance(text, 0, length, 0, length, false, length - 3);
	float advance5 = paint.getRunAdvance(text, 0, length, 0, length, false, length - 4);
	float advance6 = paint.getRunAdvance(text, 0, length, 0, length, false, length - 5);
![](https://user-gold-cdn.xitu.io/2017/7/24/9395717a1a0799f478f53970432c0ff1?imageView2/0/w/1280/h/960/ignore-error/1)

#### 2.2.7.2 getOffsetForAdvance(CharSequence text,int start,int end,int contextStart,int contextEnd,boolean isRtl,float advance)
	给出一个位置的像素值，计算出文字中最接近这个位置的字符偏移量。即第几个字符最接近这个坐标
	advance 计算出偏移量的返回值
	
	getOffsetForAdvance()配合上getRunAdvance()一起使用，就可以实现获取用户点击处的文字坐标的需求了。

### 2.2.8 hasGlyph(String string)
	检查指定的字符串中是否是一个单独的字形（glyph）。最简单的情况是，string只有一个字母。
![](https://user-gold-cdn.xitu.io/2017/7/24/c86dc73afdcba57720be17af873b302d?imageView2/0/w/1280/h/960/ignore-error/1)

