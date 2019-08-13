﻿﻿﻿﻿﻿﻿﻿﻿﻿GitHub下载慢可以[前往码云](https://gitee.com/BWmelon/qrcode)下载﻿﻿﻿﻿﻿﻿﻿qq微信支付宝三合一在线生成 - 自定义收款码颜色 - 二维码简化演示网站：[https://qr.no0a.cn](https://qr.no0a.cn)## 前言最初接触到收款码三合一是芝麻收款，刚开始是免费的，后来价格变成了5rmb生成一次。之后用过两个收款码生成系统，一个是[收款啦](https://qr.52ecy.cn/) ，还有一个是[优启梦收款码](https://qrpay.uomg.com/)，前面一个用起来挺方便的，就是二维码识别得比较慢，自己想改接口但是没学过php也做不了什么。后面一个是买的源码，用了一段时间提示什么小媳妇让我把你站禁了(￣▽￣)~*，找了作者之后前一段时间又提示让买源码。。。想把他这个限制给取消了，但是刚看完html+css教程的我只能束手无策，于是就萌生了自己搞一个生成系统的想法。前前后后弄了几个星期，基本上是在边百度边看文档中度过的，因为刚学这个，很多东西也没接触过。把这个系统功能分析了一下，觉得这个全靠html+css+js可以实现，然后就开始百度一步一步实现需求了。## 原理分析之后发现只需要两个页面。 - 生成页面 这个就是网站主页面，有两个功能，一个是上传qq、微信、支付宝收款码并将它们解析成链接，还有一个是将这几个链接合起来，然后生成合并之后的二维码。解析和生成都是用了jQuery的`qrcode`插件，为了美观，用`canvas`绘制收款码的样式。 - 收款页面 当移动设备扫描了之前生成的收款码，这个页面被打开并会获取收款码中传入的三个参数（qq、微信、支付宝链接），然后根据浏览器UA判断当前是什么软件扫的二维码，qq和微信不能直接唤起支付，这时显示二维码界面供用户长按付款，支付宝可以直接进去转账页面。这样的话这个网站就做好了，生成页面借鉴了[收款啦](https://qr.52ecy.cn/) 和 [优启梦收款码](https://qrpay.uomg.com/)，为了不太单调而且不把他们的功能生搬硬套的弄过来，想了一会就弄了个换色的功能(感觉没什么用，完全是凑内容的哈哈)，如果需要其他样式的话，可以去他们的网站生成。还有因为这三个收款码链接加起来特别长，生成的二维码比较密集（也就是丑），然后就通过[~~suo.im~~](http://suo.im/)新浪短网址将长网址缩短，这样生成的二维码就会简单一点。## 使用 1. 下载源码，上传到自己的服务器或虚拟主机。 2. 打开index.html，选择引用图片的方式，默认为引用淘宝图片，速度快。如果不想使用淘宝图片，可以使用引用本地图片方式，文件中已注明。 2. 在`/js/index.js`中更换自己的支付宝红包码和红包口令，如不需要生成界面的红包广告则删除相关代码，文件中已标明。  如果遇到什么问题的话请反馈，虽然我也不一定能解决ヾ(๑╹◡╹)ﾉ"## 添加自定义新样式1、添加样式背景图- 使用外部图片链接方式，如淘宝链接：上传图片到各大图床，如淘宝图床，然后获取图片链接，然后在index.html 页面中 `"swiper-wrapper"` 类下添加代码：`<div class="swiper-slide" style="background-image:url(这是外部图片链接)" mould-name="new"></div>`其中`mould-name="new">`中的`new`为自定义样式名。- 使用本地图片方式：将背景图添加到 ./imgs/bgimgs/ 文件夹下，文件名以 "new.png" 为例，然后在 index.html 页面中 `"swiper-wrapper"` 类下添加样式：`<div class="swiper-slide" style="background-image:url(imgs/bgimgs/new.png)"></div>`其中的`new`也为样式名。2、打开根目录下 config.json 文件，添加json数据，根节点名必须为样式名，如 "new"，其他子节点参考下表：| 参数名 | 类型 | 说明 | 参考 || ------ | ------ | ------ | ------ || qrWidth | 整数 | 二维码宽度 | 300| qrHeight | 整数 | 二维码高度，建议和二维码宽度相同 | 300| foreground | 字符串 | 二维码前景色，支持十六进制、rgb、rgba | "#000", "rgb(0, 0, 0)", "rgba(0, 0, 0, 0.5)"| background | 字符串 | 二维码背景色，支持十六进制、rgb、rgba |  "#fff", "rgb(255, 255, 255)", "rgba(255, 255, 255, 0.5)"| imgWidth | 整数 | 背景图宽度 | 900（其他尺寸未兼容）| imgHeight | 整数 | 背景图高度 | 1200（其他尺寸未兼容）| font | 字符串 | 字体和大小 | "70px '黑体'"| fontColor | 字符串 | 文字颜色（未填写收款名则不生成） |  "#fff", "rgb(255, 255, 255)", "rgba(255, 255, 255, 0.5)"| recNameLeft | 空串或整数 | 文字距离左侧距离，建议为空串，此时文本将自适应居中显示 | "", 100| recNameTop | 整数 | 文字距离顶部距离 | 170| qrLeft | 整数 | 二维码距离左侧距离 | 270| qrTop | 整数 | 二维码距离顶部距离 | 320这样就成功添加了一个新的样式，新增的json内容内容大致为下图所示(图片中写错了，应该是`new`而不是`new.png`)：![参考](https://imgs.bwmelon.com/20190703230133.png)3、小提示：如果不想在背景中生成收款名，可以将fontColor属性设为transparent。如需修改样式滑动效果，可以参考[Swiper中文网](https://www.swiper.com.cn/api/index.html)文档。## 演示**PC端：**可以使用拖动图片或者滑动滚轮选择样式![PC端](https://imgs.bwmelon.com/20190703222357.gif)**移动端：**仅可拖动图片选择样式![移动端](https://imgs.bwmelon.com/20190703222427.gif)## 感激* [收款啦](https://qr.52ecy.cn/) * [优启梦收款码](https://qrpay.uomg.com/)* [Layui](https://www.layui.com/)部分样式来源于芝麻收款和第九工场，如有侵权，请联系删除。