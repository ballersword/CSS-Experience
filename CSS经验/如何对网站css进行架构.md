# 写在前面的
都是自己积累形成的一些东西，可能带有明显的个人印记。不是专业内容，不是权威指南，只是展示一点自己的观点，借此希望能与各位优秀的同行交流看法，见解。以得到进步与提高。

# 我所知的一些过往的做法
关于如何处理网站的CSS，各个网站做法都不一样，这随着网站的性质及大小不同，公司前人留下的规范不同，以及CSS工程师的眼界不同而有所不同。由于我从业经历有限，所知甚浅，只能说些肤浅业余的内容，不准确之处欢迎指出。

就CSS文件而言，有的网站分为header.css, body.css, footer.css，不做评价；  
有的分为reset.css, main.css, content.css，不做评价；  
有的分为common.css,然后每个种类的页面一个CSS，例如home.css(主页), album.css(相册页面),message.css(站内信页面),blog.css(日志页面)等，不做评价；  
有的分为base.css，然后每个活动页面一个单独的CSS，等，不做评价；  
还有的直接将CSS嵌在页面中，而非外部链接调用，不做评价。  

这些不同的处理方法，没有什么正确与错误之分，只有适合不适合。每种方法都有其存在的道理，所以我是没有资格做任何评价的。

就每个CSS文件的内容而言，一般都会有一段长长的CSS reset（样式重置），然后就是有着统一前缀，命名较长的样式内容，就像人人网的部分样式截图：
人人网长命名的CSS代码 张鑫旭-鑫空间-鑫生活

使用长命名，统一的父级命名避免样式冲突时无可厚非的。确实！曾经我也如此。

# 我是如何对网站CSS进行架构的
首先关于CSS文件，我一般只使用一个文件，这无关于网站的大小，网站越大，某种意义上我这种做法的优势与潜力就会体现的越明显。我这种单CSS文件的做法适合于web2.0的网站，例如像是SNS网站（开心、人人、白社会），嘀咕网，虾米网，凡客这类网站，如果是门户网站，sorry，铁定不适合。

让网站单CSS谁都会，关键是为何可以使用单CSS文件，这个CSS文件不会很大吗，如果一个网站有400个页面，那么这个CSS文件岂不要数百K。非也，在网站页面风格一致，在web系统结构良好的情况下，CSS文件可以控制的非常小，而且高性能，同时页面扩展性也非常好。下面就开始一点一点的展示，内容较多，需要慢慢来~~

1. 整体概述
页面布局与文章内容显示需要，我将整体架构做成了一张图片，见下图：
张鑫旭的CSS架构内容示意图 张鑫旭-鑫空间-鑫生活

2. 关于CSS reset
CSS reset(css重置)基本上是不需要的，至少可以说80%的的CSS reset都是没有必要的，反而增加了页面CSS 的overwrite，尤其像开心网*{margin:0;}这样子业余的做法更是要不得（反而破坏了很多UI的兼容性，比如说单复选框等）。我不是一概鄙弃CSS reset，有些常用标签我也是会简单重置一下的，而且会避免overwrite（样式重写），以保证样式最精简，渲染最高效。如下代码示例：

~~~
body{ line-height:1.4; color:#333; font-family:arial; font-size: 12px; background:white;}
input,textarea,select{ font-size:12px;font-size:100%;     font-family:arial;font-family:inherit;}
body,h1,h2,h3,h4,h5,h6,p,ul,ol,form{ margin:0;}
h4,h5,h6{ font-size:1em;}
ul,ol{padding-left:0; list-style-type:none;}
/*image with no-border*/
a img{border:0;}
img{border:0;}
~~~

这就是我全部的CSS reset。就这些就足够了，我是没有遇到什么兼容性的问题，不要盲从于一些主流的做法，就这些，足够了。

3. 关于CSS通用样式库
我在“CSS样式分离之再分离”一文中曾提到过CSS通用样式库。所谓CSS通用样式库就是可以在任何网站使用的CSS样式库。“CSS样式分离之再分离”一文中仅仅展示了CSS同样样式库的一部分，完整的通用样式库如下（您可以根据自己的喜好重命名或是添加删除部分样式）：

~~~
.l{float:left;}.r{float:right;}.cl{clear:both;}
.n{font-weight:normal; font-style:normal;}.b{font-weight:bold;}.i{font-style:italic;}
.fa{font-family:Arial;}.fg{font-family:Georgia;}.ft{font-family:Tahoma;}.fl{font-family:Lucida Console;}.fs{font-family:'宋体';}.fw{font-family:'微软雅黑';}
.tc{text-align:center;}.tr{text-align:right;}.tl{text-align:left;}
.tdl{text-decoration:underline;}.tdn,.tdn:hover,a.tdl:hover{text-decoration:none;}
.g0{color:#000000;}.g3{color:#333333;}.g6{color:#666666;}.g9{color:#999999;}.red{color:red;}.wh{color:white;}
.f0{font-size:0;}.f10{font-size:10px;}.f12{font-size:12px;}.f13{font-size:13px;}.f14{font-size:14px;}.f16{font-size:16px;}.f20{font-size:20px;}.f24{font-size:24px;}
.vm{vertical-align:middle;}.vtb{vertical-align:text-bottom;}.vt{vertical-align:top;}.vn{vertical-align:-2px;}.vimg{margin-bottom:-3px;}
.m0{margin:0;}.ml1{margin-left:1px;}.ml2{margin-left:2px;}.ml5{margin-left:5px;}.ml10{margin-left:10px;}.ml20{margin-left:20px;}.mr1{margin-right:1;}.mr2{margin-right:2px;}.mr5{margin-right:5px;}.mr10{margin-right:10px;}.mr20{margin-right:20px;}.mt1{margin-top:1;}.mt2{margin-top:2px;}.mt5{margin-top:5px;}.mt10{margin-top:10px;}.mt20{margin-top:20px;}.mb1{margin-bottom:1px;}.mb2{margin-bottom:2px;}.mb5{margin-bottom:5px;}.mb10{margin-bottom:10px;}.mb20{margin-bottom:20px;}.ml-1{margin-left:-1px;}.mt-1{margin-top:-1px;}
.p1{padding:1px;}.pl1{padding-left:1px;}.pt1{padding-top:1px;}.pr1{padding-right:1px;}.pb1{padding-bottom:1px;}.p2{padding:2px;}.pl2{padding-left:2px;}.pt2{padding-top:2px;}.pr2{padding-right:2px;}.pb2{padding-bottom:2px;}.pl5{padding-left:5px;}.p5{padding:5px;}.pt5{padding-top:5px;}.pr5{padding-right:5px;}.pb5{padding-bottom:5px;}.p10{padding:10px;}.pl10{padding-left:10px;}.pt10{padding-top:10px;}.pr10{padding-right:10px;}.pb10{padding-bottom:10px;}.p20{padding:20px;}.pl20{padding-left:20px;}.pt20{padding-top:20px;}.pr20{padding-right:20px;}.pb20{padding-bottom:20px;}
.rel{position:relative;}.abs{position:absolute;}
.dn{display:none;}.db{display:block;}.dib{-moz-inline-stack:inline-block; display:inline-block;}.di{display:inline;}
.ovh{overflow:hidden;}.ovs{overflow:scroll;}.vh{visibility:hidden;}.vv{visibility:visible;}
.lh14{line-height:14px;}.lh16{line-height:16px;}.lh18{line-height:18px;}.lh20{line-height:20px;}.lh22{line-height:22px;}.lh24{line-height:24px;}
.fix{*zoom:1;}.fix:after,.fix:before{display:block; content:"clear"; height:0; clear:both; overflow:hidden; visibility:hidden;}.z{_zoom:1;}
~~~

上面的样式是有简单的分类的，某种意义上讲，CSS库与js库属于类似的东西。

关于此样式库，您可以直接在您的页面头部<head>标签内嵌入如下代码：
~~~
<link rel="stylesheet" href="./css/zxx.lib.css" type="text/css" />
~~~
如果您想下载此CSS文件，您可以狠狠地点击这里：zxx.lib.css(右键-[目标|链接另存为])。您可以随意修改，如果能保留我的一个个人信息，那真是感激不尽~~

>更新：已开源到github上了：https://github.com/zhangxinxu/zxx.lib.css

4. 网站CSS样式库

这里的样式是根据当前实际的项目内容指定的。例如，文字链接颜色是什么，文字链接经过的样式是什么；一些常用的背景色样式，常用的边框样式等，以及一些高宽等。按照我的经验，网站CSS样式库又可以架构为以下几部分：

- 网站常见颜色，尤其是链接色
- 网站常见背景色（我习惯用bg+颜色前2字母表示，例如.bgf7表示background:#f7f7f7）
- 网站常见边框色，这里类似于CSS 通用库中的margin属性，需拆分，例如.bbdd表示border-bottom:1px solid #ddd;每人的命名习惯不一样，但是尽量简单为好，甚至您可以像Google一样，直接两个字母（大小写混搭）表示。另外，一定要告知设计师，边框取色不宜多，不能凭感觉，要有所牺牲，也就是如果之前使用了#cecece的边框色，后面的#d0d0d0颜色与之相近，请可以使用#cecece代替，用户是看不出来其中差异的。
- 网站遗留的单margin属性，例如，某一div留白较大，有个单独的margin-top:35px的属性，OK，这个属性请放在网站CSS样式库中，以.mt35{margin-top:35px;}保留，以供之后类似布局或需要的地方使用。
- 网站遗留的单padding属性，例如，双栏自适应布局时，无论是浮动自适应，还是绝对定位自适应，都需要使用padding-left值，此时的padding-left多单样式，可抽取出来，以网站样式库的形式存在。记住，是单属性，且不可从通用元素中抽取单独的padding值，否则是给自己挖火坑。
- 网站已有的width属性，在流体布局思想下，宽度是有限的，是珍贵的，需好好利用。
- 网站常用的一些height属性，指一些高度值，例如height:18px，height:20px，height:24px，height:50px，height:100px，height:200px等。

记住一个原则：**网站通用的元素（按钮，导航，选项卡的）的样式千万不能分离作为网站的CSS样式库**

5. 网站通用小图标样式集
小图标的样式合并是普遍处理的较好的，由于其规律可循，所以经常在CSS文件较上的位置看到有关小图标的CSS合并样式，这在SNS网站中很是常见。一般合并样式部分样式为{background:url(xx.png) no-repeat;}，分离部分的样式是{background-position:x, y;}，就实现而言，我觉得没有多少说头，只是命名有些自己的见解。在小图标样式命名的时候，我的建议是不要关联图片的内容，比如说一个相册的下图标，不应该使用iAlbum这样的命名。原因有三：

- 思考图片的命名杀死n多脑细胞
- 命名较长，占用字节数，也就是CSS文件大小
- 也是最重要的，后期的维护。设想下，如果日后相册的图标不再被使用了，原来相册图标的位置可以被其他小图标（如RSS小图标）替换吗？理论上可以，实际上，我们除了必要的html替换，还需要重新修改图标样式的命名，即iAlbum→iRss的命名，而往往取而代之的做法是直接在后面添加新的图标。

我目前的做法是使用一个不常用的标签作为网站的小图标专用标签，例如s标签，或是u标签，我习惯将小图标单独为一个小图标Sprite，每个图标放在20*20像素的格子中。在这种情况下，我都是使用矩阵命名法。命名只关联位置，例如，我使用u标签作为整个网站的小图标专用标签，则按照图标的位置（假设一行20个图标），我会依次命名为：u00,u01,u02…u019,u10,u11,…u119…。这种命名的好处是不用关心到底哪个位置是那个图标，不用担心命名冲突，在小图标位置以及内容更换的情况下也无需重命名。

例如，上图中标注的u113的意思其实是u(1,13)，这种小图标命名的方法我称之为“小图标矩阵命名法”。此命名略有不足在于在使用小图标时需要打开源文件或通过注释准确查询到对应的class。

6. 网站通用样式
这里的“网站通用样式”可以说与“网站通用样式库”最为对立的两部分。网站通用样式专指“独立元素”的通用样式，所谓“独立元素”指的是网站通用的导航，菜单，按钮，选项卡，文本框装饰，图片装饰，圆角处理等等。这些“独立元素”的样式千万不能对其进行分离并归入“网站通用样式库”中，否则，日后会给你留下无尽的痛苦的！

我几乎从不对按钮或是导航进行定宽，都是宽度自适应，这样，可以大大节约Sprite背景图片以及CSS代码的成本。以前多有探讨，这里不多说了。

网站通用样式的代码量在整个CSS文件中所占据的比重是相当大的，如果您的CSS文件中发现CSS通用样式只占整个CSS文件的一小部分，尤其网站项目较大时，那就需要引起警惕，可能最后的结果就是CSS文件超负荷，最后反而一团糟。

7. 网站公共结构样式
所谓“网站的结构样式”主要指的是最外框div的样式，一般限制网站的宽度(960~990不等)，还有就是网站的分栏布局样式，这里的样式仅仅针对主体结构，例如left_part，或是right_part；还包括网站的头部的一些公用结构，底部的样式结构等。

我是强烈建议公共结构仅仅定宽定高，设置浮动属性，切不可在结构样式上添加margin或是padding属性，这会使网站的公共结构的重用性大大降低！

8. 单页面的精细结构
如果上述您都架构的非常好，那么您在编写每个具体页面的时候，就会非常轻松，非常迅速。因为80%~90%的样式都可以从上面11项中直接拿来用（上述11项全部都是网站公用样式）。

对于中型大型网站，我们可能要花3~4天甚至更多的时间分析页面设计图，处理CSS Sprite，架构网站的CSS，这段时间不写任何页面，就是处理网站（可以说是）唯一的CSS文件。所谓“磨刀不误砍柴功”，站在整站的角度上去思考CSS是非常重要的，这可以让你避免迷路，有助于写出精简高效的样式代码。

当我们把所有都完成了，就开始着手写页面了，这时候，整个网站的页面基本上都在你脑中了，您在下手的时候就会清除：我现在做的是哪个页面，在整个网站中扮演着什么样的地位，这个页面的CSS对整个网站的CSS有什么影响，这里的样式该怎么处理（分离，合并还是独立）等。

一般而言，就我个人经验，每个页面，即使这个页面看上去很复杂，其代码开销也是非常小的。其新增的代码开销去处有三处：一是分离一些样式归入“网站CSS样式库”中；二是凡事使用的CSS Sprite的样式与其他样式进行合并；三就是一些精细的复杂的样式，这些就是CSS文件的架构的最后一部分“单页面的精细结构了”，何为单页面的精细结构，如下图的样式，就可以说是精细结构，需要独立出来新写样式



# 关于适用性
有些东西虽然看上去好，但是却不适用。通过上述的CSS架构，我可以把网站的样式控制地非常的精简与高效（当然，需要设计师与后台工程师的通力配合），但是，对于别人，套用此架构可能就没有这样的效果，可能反而会更糟。前面也提到了，这种架构是我自己摸索出来的，是根据自己的写法，布局思想，甚至性格等形成的，带有明显的个人印记。

比方说，我是个推崇自适应布局（流体布局）的人，是个十足的自适应控，但是，有很大一部分同行是固定布局（像素级兼容，有计算）。固定布局固然有其优点，但是其CSS代码的消耗量以及页面的扩展性我是很诟病的，显然，这是无法应用到我这里的架构中的。

其次，不少CSS刚入门的页面开发工程师对CSS属性理解不够透彻，常会写一些没有必要的冗余代码。对于他们而言，但CSS文件的架构确实很吃力。

说实话，我对自己的这个CSS架构的适应性都不看好，一是自己在表达方面的火候欠缺，没有很好的展示架构的精髓，二是因为此架构本身需要有很多的控制，这种控制受制于设计师，网站页面架构，CSS工程师自身的功力，一旦样式泛滥，这种架构也就毫无意义，反而弄巧成拙；但是，一旦控制下来，那么网站就CSS性能这块保证领先，而这些需要优秀的有眼界的CSS工程师来掌控，需要优秀的设计师，程序员通力协作。虽然全然套用我展示的这套架构会由于不熟悉或是掌控不够而产生问题，但是，里面一些概念，一些思想应该能有一定的启示作用的，这也是本文的意义所在了。
 