---
title: "Tkinter 使用记录 python-GUI"
date: 2019-01-31T17:19:19.657+08:00
lastmod: 2019-01-31T17:19:19.657+08:00
draft: false
tags: [“tkinter”]
categories: ["python", "课余"]
author: "Tonser"

# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
# comment: false
# toc: false
# reward: false
# mathjax: true
---
在使用python 写gui时 使用tkinter非常方便，下面是一些记录
<!--more-->


## 版本

python版本：3.6.5

自带 tkinter

## Entry使用方法

直接通过样例去认识就足够了

```python
import tkinter
root=tkinter.Tk() #生成root主窗口
label=tkinter.Label(root,text='Hello,GUI') #生成标签
label.pack()        #将标签添加到主窗口
button1=tkinter.Button(root,text='Button1') #生成button1
button1.pack(side=tkinter.LEFT)         #将button1添加到root主窗口
button2=tkinter.Button(root,text='Button2')
button2.pack(side=tkinter.RIGHT)
root.mainloop()             #进入消息循环（必需组件）
```

## Tkinter的15个核心组件

```
    Button        　　按钮；
    Canvas        　　绘图形组件，可以在其中绘制图形；
    Checkbutton      复选框；
    Entry        　　 文本框（单行）；
    Text             文本框（多行）；
    Frame         　　框架，将几个组件组成一组
    Label        　　 标签，可以显示文字或图片；
    Listbox      　　 列表框；
    Menu     　　     菜单；
    Menubutton       它的功能完全可以使用Menu替代；
    Message          与Label组件类似，但是可以根据自身大小将文本换行；
    Radiobutton      单选框；
    Scale      　　   滑块；允许通过滑块来设置一数字值
    Scrollbar        滚动条；配合使用canvas, entry, listbox, and text窗口部件的标准滚动条；
    Toplevel         用来创建子窗口窗口组件。
（在Tkinter中窗口部件类没有分级；所有的窗口部件类在树中都是兄弟。）
```

## Tkinter 组件的放置与排版（pack，grid，place）

```
pack组件设置位置属性参数：
    after:    　　　 将组件置于其他组件之后；
    before:    　　　将组件置于其他组件之前；
    anchor:    　　  组件的对齐方式，顶对齐'n',底对齐's',左'w',右'e'
    side:    　　　　组件在主窗口的位置，可以为'top','bottom','left','right'（使用时tkinter.TOP,tkinter.E）；
    fill            填充方式 (Y,垂直，X，水平）
    expand          1可扩展，0不可扩展
grid组件使用行列的方法放置组件的位置，参数有：
    column:         组件所在的列起始位置；
    columnspam:     组件的列宽；
    row：      　　　组件所在的行起始位置；
    rowspam：    　　组件的行宽；
place组件可以直接使用坐标来放置组件，参数有：
    anchor:    　　　组件对齐方式；
    x:        　　　 组件左上角的x坐标；
    y:        　　   组件右上角的y坐标；
    relx:         　组件相对于窗口的x坐标，应为0-1之间的小数；
    rely:           组件相对于窗口的y坐标，应为0-1之间的小数；
    width:          组件的宽度；
    heitht:    　   组件的高度；
    relwidth:       组件相对于窗口的宽度，0-1；
    relheight:　    组件相对于窗口的高度，0-1；
```

## 使用tkinter.Button时控制按钮的参数

```
    anchor:      　　　　  指定按钮上文本的位置；
    background(bg)    　  指定按钮的背景色；
    bitmap:       　　　　 指定按钮上显示的位图；
    borderwidth(bd)　　　　指定按钮边框的宽度；
    command:   　　　　　  指定按钮消息的回调函数；
    cursor:        　　　　指定鼠标移动到按钮上的指针样式；
    font:           　　  指定按钮上文本的字体；
    foreground(fg)　　　　 指定按钮的前景色；
    height:        　　　　指定按钮的高度；
    image:        　　　　 指定按钮上显示的图片；
    state:          　　　 指定按钮的状态（disabled）；
    text:           　　　 指定按钮上显示的文本；
    width:       　　　　  指定按钮的宽度
    padx          　　　　 设置文本与按钮边框x的距离，还有pady;
    activeforeground　　　 按下时前景色
    textvariable    　　  可变文本，与StringVar等配合着用
```
## 文本框tkinter.Entry,tkinter.Text控制参数

```
    background(bg)   　　 文本框背景色；
    foreground(fg)        前景色；
    selectbackground　　  选定文本背景色；
    selectforeground　　  选定文本前景色；
    borderwidth(bd)    　 文本框边框宽度；
    font                　字体；
    show          　　    文本框显示的字符，若为*，表示文本框为密码框；
    state            　　 状态；
    width        　　　　  文本框宽度
    textvariable    　　  可变文本，与StringVar等配合着用
```
## 标签tkinter.Label组件控制参数

```
    background(bg)   　　 文本框背景色；
    foreground(fg)        前景色；
    selectbackground　　  选定文本背景色；
    selectforeground　　  选定文本前景色；
    borderwidth(bd)    　 文本框边框宽度；
    font                　字体；
    show          　　    文本框显示的字符，若为*，表示文本框为密码框；
    state            　　 状态；
    width        　　　　  文本框宽度
    textvariable    　　  可变文本，与StringVar等配合着用
```

## 单选框和复选框Radiobutton,Checkbutton控制参数
```
    anchor         　　文本位置；
    background(bg) 　　背景色；
    foreground(fg)    前景色；
    borderwidth       边框宽度；
    width        　　  组件的宽度；
    height     　　    组件高度；
    bitmap    　　     组件中的位图；
    image    　　      组件中的图片；
    font       　　    字体；
    justify       　　 组件中多行文本的对齐方式；
    text         　　  指定组件的文本；
    value      　　    指定组件被选中中关联变量的值；
    variable     　    指定组件所关联的变量；
    indicatoron        特殊控制参数，当为0时，组件会被绘制成按钮形式;
    textvariable       可变文本显示，与StringVar等配合着用
```

## 组图组件Canvas控制参数

```
    background(bg)  　　  背景色;
    foreground(fg)       前景色;
    borderwidth   　　　　组件边框宽度；
    width     　　　　    组件宽度；
    height     　　      高度;
    bitmap 　　          位图;
    image 　　　　        图片;
    绘图的方法主要以下几种：
    create_arc          圆弧;
    create_bitmap  　　  绘制位图，支持XBM;
    create_image    　　 绘制图片，支持GIF(x,y,image,anchor);
    create_line         绘制支线；
    create_oval;        绘制椭圆；
    create_polygon   　　绘制多边形(坐标依次罗列，不用加括号，还有参数，fill,outline)；
    create_rectangle　　 绘制矩形((a,b,c,d),值为左上角和右下角的坐标)；
    create_text         绘制文字(字体参数font,)；
    create_window    　　绘制窗口；
    delete            　 删除绘制的图形；
    itemconfig          修改图形属性，第一个参数为图形的ID，后边为想修改的参数；
    move          　　   移动图像（1，4，0），1为图像对象，4为横移4像素，0为纵移像素，然后用root.update()刷新即可看到图像的移动，为了使多次移动变得可视，最好加上time.sleep()函数；
    只要用create_方法画了一个图形，就会自动返回一个ID,创建一个图形时将它赋值给一个变量，需要ID时就可以使用这个变量名。
    coords(ID)          返回对象的位置的两个坐标（4个数字元组）；

    对于按钮组件、菜单组件等可以在创建组件时通过command参数指定其事件处理函数。方法为bind;或者用bind_class方法进行类绑定，bind_all方法将所有组件事件绑定到事件响应函数上。
```

## 菜单Menu
```
参数： 
    tearoff      　   分窗，0为在原窗，1为点击分为两个窗口
    bg,fg       　　  背景，前景
    borderwidth    　 边框宽度
    font              字体
    activebackgound   点击时背景，同样有activeforeground，activeborderwidth，disabledforeground
    cursor
    postcommand
    selectcolor    　 选中时背景
    takefocus
    title       
    type
    relief
   
方法：
    menu.add_cascade      添加子选项
    menu.add_command      添加命令（label参数为显示内容）
    menu.add_separator    添加分隔线
    menu.add_checkbutton  添加确认按钮
    delete                删除
```

## 事件关联
```
bind(sequence,func,add)——
bind_class(className,sequence,func,add)
bind_all(sequence,func,add)
事件参数：　　
sequence      　　　　　　　　所绑定的事件；
func            　　　　　　 所绑定的事件处理函数；
add             　　　　　　 可选参数，为空字符或‘+’；
className    　　　　　　　 　所绑定的类；

鼠标键盘事件
    <Button-1>        　  　鼠标左键按下，2表示中键，3表示右键；
    <ButtonPress-1>    　   同上；
    <ButtonRelease-1>　　　 鼠标左键释放；
    <B1-Motion>  　　       按住鼠标左键移动；
    <Double-Button-1>  　　 双击左键；
    <Enter>       　　      鼠标指针进入某一组件区域；
    <Leave>    　　         鼠标指针离开某一组件区域；
    <MouseWheel>  　   　　 滚动滚轮；
    <KeyPress-A> 　　  　　  按下A键，A可用其他键替代；
    <Alt-KeyPress-A>　　　   同时按下alt和A；alt可用ctrl和shift替代；
    <Double-KeyPress-A>　　  快速按两下A；
    <Lock-KeyPress-A>　　　  大写状态下按A；
   
窗口事件
    Activate        　　　　 当组件由不可用转为可用时触发；
    Configure      　　　　  当组件大小改变时触发；
    Deactivate    　　　　　 当组件由可用转变为不可用时触发；
    Destroy        　　　　  当组件被销毁时触发；
    Expose         　　　　　当组件从被遮挡状态中暴露出来时触发；
    Unmap        　　　　　　当组件由显示状态变为隐藏状态时触发；
    Map         　　　　     当组件由隐藏状态变为显示状态时触发；
    FocusIn       　　　 　  当组件获得焦点时触发；
    FocusOut      　　　　　 当组件失去焦点时触发；
    Property     　　　　    当窗体的属性被删除或改变时触发；
    Visibility       　　　　当组件变为可视状态时触发；

响应事件
event对象（def function(event)）：
    char        　　　　　　  按键字符，仅对键盘事件有效；
    keycode   　　　　　　  　按键名，仅对键盘事件有效；
    keysym     　　　　　　　 按键编码，仅对键盘事件有效；
    num          　　　　　　鼠标按键，仅对鼠标事件有效；
    type         　　　　    所触发的事件类型；
    widget      　　　　     引起事件的组件；
    width,heigh　　　　　　  组件改变后的大小，仅Configure有效；
    x,y       　  　　　　　　鼠标当前位置，相对于窗口；
    x_root,y_root　　　　　　 鼠标当前位置，相对于整个屏幕
```
## 弹窗
```
messagebox._show函数的控制参数：
    default         指定消息框按钮；
    icon            指定消息框图标；
    message     　 　指定消息框所显示的消息；
    parent          指定消息框的父组件；
    title           标题；
    type            类型；

simpledialog模块参数：
    title           指定对话框的标题；
    prompt        　显示的文字；
    initialvalue    指定输入框的初始值；

　　filedialog　　　　模块参数：
    filetype   　　  指定文件类型；
    initialdir 　　  指定默认目录；
    initialfile 　　 指定默认文件；
    title    　　　  指定对话框标题

colorchooser模块参数：
    initialcolor  　 指定初始化颜色；
    title          　指定对话框标题；
```
## 字体（font)
```
一般格式：
（'Times -10 bold')
('Times',10,'bold','italic')    依次表示字体、字号、加粗、倾斜


补充：
config            重新配置
label.config(font='Arial -%d bold' % scale.get())
依次为字体，大小（大小可为字号大小），加粗
tkinter.StringVar    能自动刷新的字符串变量，可用set和get方法进行传值和取值，类似的还有IntVar,DoubleVar...

sys.stdout.flush()　　刷新输出
```
## Tkinter 中的颜色

<center>![颜色图](/image/tk_color.png)</center>

```
#FFB6C1 LightPink 浅粉红
#FFC0CB Pink 粉红
#DC143C Crimson 深红/猩红
#FFF0F5 LavenderBlush 淡紫红
#DB7093 PaleVioletRed 弱紫罗兰红
#FF69B4 HotPink 热情的粉红
#FF1493 DeepPink 深粉红
#C71585 MediumVioletRed 中紫罗兰红
#DA70D6 Orchid 暗紫色/兰花紫
#D8BFD8 Thistle 蓟色
#DDA0DD Plum 洋李色/李子紫
#EE82EE Violet 紫罗兰
#FF00FF Magenta 洋红/玫瑰红
#FF00FF Fuchsia 紫红/灯笼海棠
#8B008B DarkMagenta 深洋红
#800080 Purple 紫色
#BA55D3 MediumOrchid 中兰花紫
#9400D3 DarkViolet 暗紫罗兰
#9932CC DarkOrchid 暗兰花紫
#4B0082 Indigo 靛青/紫兰色
#8A2BE2 BlueViolet 蓝紫罗兰
#9370DB MediumPurple 中紫色
#7B68EE MediumSlateBlue 中暗蓝色/中板岩蓝
#6A5ACD SlateBlue 石蓝色/板岩蓝
#483D8B DarkSlateBlue 暗灰蓝色/暗板岩蓝
#E6E6FA Lavender 淡紫色/熏衣草淡紫
#F8F8FF GhostWhite 幽灵白
#0000FF Blue 纯蓝
#0000CD MediumBlue 中蓝色
#191970 MidnightBlue 午夜蓝
#00008B DarkBlue 暗蓝色
#000080 Navy 海军蓝
#4169E1 RoyalBlue 皇家蓝/宝蓝
#6495ED CornflowerBlue 矢车菊蓝
#B0C4DE LightSteelBlue 亮钢蓝
#778899 LightSlateGray 亮蓝灰/亮石板灰
#708090 SlateGray 灰石色/石板灰
#1E90FF DodgerBlue 闪兰色/道奇蓝
#F0F8FF AliceBlue 爱丽丝蓝
#4682B4 SteelBlue 钢蓝/铁青
#87CEFA LightSkyBlue 亮天蓝色
#87CEEB SkyBlue 天蓝色
#00BFFF DeepSkyBlue 深天蓝
#ADD8E6 LightBlue 亮蓝
#B0E0E6 PowderBlue 粉蓝色/火药青
#5F9EA0 CadetBlue 军兰色/军服蓝
#F0FFFF Azure 蔚蓝色
#E0FFFF LightCyan 淡青色
#AFEEEE PaleTurquoise 弱绿宝石
#00FFFF Cyan 青色
#00FFFF Aqua 浅绿色/水色
#00CED1 DarkTurquoise 暗绿宝石
#2F4F4F DarkSlateGray 暗瓦灰色/暗石板灰
#008B8B DarkCyan 暗青色
#008080 Teal 水鸭色
#48D1CC MediumTurquoise 中绿宝石
#20B2AA LightSeaGreen 浅海洋绿
#40E0D0 Turquoise 绿宝石
#7FFFD4 Aquamarine 宝石碧绿
#66CDAA MediumAquamarine 中宝石碧绿
#00FA9A MediumSpringGreen 中春绿色
#F5FFFA MintCream 薄荷奶油
#00FF7F SpringGreen 春绿色
#3CB371 MediumSeaGreen 中海洋绿
#2E8B57 SeaGreen 海洋绿
#F0FFF0 Honeydew 蜜色/蜜瓜色
#90EE90 LightGreen 淡绿色
#98FB98 PaleGreen 弱绿色
#8FBC8F DarkSeaGreen 暗海洋绿
#32CD32 LimeGreen 闪光深绿
#00FF00 Lime 闪光绿
#228B22 ForestGreen 森林绿
#008000 Green 纯绿
#006400 DarkGreen 暗绿色
#7FFF00 Chartreuse 黄绿色/查特酒绿
#7CFC00 LawnGreen 草绿色/草坪绿
#ADFF2F GreenYellow 绿黄色
#556B2F DarkOliveGreen 暗橄榄绿
#9ACD32 YellowGreen 黄绿色
#6B8E23 OliveDrab 橄榄褐色
#F5F5DC Beige 米色/灰棕色
#FAFAD2 LightGoldenrodYellow 亮菊黄
#FFFFF0 Ivory 象牙色
#FFFFE0 LightYellow 浅黄色
#FFFF00 Yellow 纯黄
#808000 Olive 橄榄
#BDB76B DarkKhaki 暗黄褐色/深卡叽布
#FFFACD LemonChiffon 柠檬绸
#EEE8AA PaleGoldenrod 灰菊黄/苍麒麟色
#F0E68C Khaki 黄褐色/卡叽布
#FFD700 Gold 金色
#FFF8DC Cornsilk 玉米丝色
#DAA520 Goldenrod 金菊黄
#B8860B DarkGoldenrod 暗金菊黄
#FFFAF0 FloralWhite 花的白色
#FDF5E6 OldLace 老花色/旧蕾丝
#F5DEB3 Wheat 浅黄色/小麦色
#FFE4B5 Moccasin 鹿皮色/鹿皮靴
#FFA500 Orange 橙色
#FFEFD5 PapayaWhip 番木色/番木瓜
#FFEBCD BlanchedAlmond 白杏色
#FFDEAD NavajoWhite 纳瓦白/土著白
#FAEBD7 AntiqueWhite 古董白
#D2B48C Tan 茶色
#DEB887 BurlyWood 硬木色
#FFE4C4 Bisque 陶坯黄
#FF8C00 DarkOrange 深橙色
#FAF0E6 Linen 亚麻布
#CD853F Peru 秘鲁色
#FFDAB9 PeachPuff 桃肉色
#F4A460 SandyBrown 沙棕色
#D2691E Chocolate 巧克力色
#8B4513 SaddleBrown 重褐色/马鞍棕色
#FFF5EE Seashell 海贝壳
#A0522D Sienna 黄土赭色
#FFA07A LightSalmon 浅鲑鱼肉色
#FF7F50 Coral 珊瑚
#FF4500 OrangeRed 橙红色
#E9967A DarkSalmon 深鲜肉/鲑鱼色
#FF6347 Tomato 番茄红
#FFE4E1 MistyRose 浅玫瑰色/薄雾玫瑰
#FA8072 Salmon 鲜肉/鲑鱼色
#FFFAFA Snow 雪白色
#F08080 LightCoral 淡珊瑚色
#BC8F8F RosyBrown 玫瑰棕色
#CD5C5C IndianRed 印度红
#FF0000 Red 纯红
#A52A2A Brown 棕色
#B22222 FireBrick 火砖色/耐火砖
#8B0000 DarkRed 深红色
#800000 Maroon 栗色
#FFFFFF White 纯白
#F5F5F5 WhiteSmoke 白烟
#DCDCDC Gainsboro 淡灰色
#D3D3D3 LightGrey 浅灰色
#C0C0C0 Silver 银灰色
#A9A9A9 DarkGray 深灰色
#808080 Gray 灰色
#696969 DimGray 暗淡灰
#000000 Black 纯黑
```