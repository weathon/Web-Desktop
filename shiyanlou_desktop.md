# 实验楼教程编写模板及实例
#投稿须知

1. 教程必须为作者本人原创，不涉及到其他版权问题，有参考他人或开源项目的内容必须在教程中详细列出。
2. 教程必须在实验楼环境可实现（Ubuntu Linux 14.04桌面环境）。
3. 教程应达到边学边练，需在实践操作中穿插理论知识点讲解，至少包含3个知识点。
4. 教程需为 _markdown_ 格式文件，也可直接发送教程博文链接。
5. 有任何不清楚的地方欢迎与我们联系
 QQ：  3185057317
Email: yandan@simplecloud.cn 

#投稿方式

发送 常用QQ号+昵称+教程+授权文字 到yandan@simplecloud.cn快速投稿。
授权文字：为了尊重作者版权、保护作者利益，需要在投稿邮件中附上以下授权文字（粘贴到邮件中即可）：
> 我谨保证我是此教程的著作权合法人，我同意“实验楼”所属网站和媒体发布此教程，允许将此教程发布到实验楼的免费课或会员课中。未经实验楼或本人同意，其他机构、媒体一律不得转载、使用。  

#教程模板

## 一、实验介绍
### 1.1 实验内容
利用Web技术开发一个虚拟的桌面

### 1.2 实验知识点 

- HTML、CSS、JS基本操作

- 简单第三方库的使用

### 1.3 实验环境
- 支持最新HTML标准的浏览器

- 文本编辑器

### 1.4 适合人群
计算机和Web技术初学者

### 1.5 代码获取

```bash
git clone https://github.com/weathon/Web-Desktop.git
```

## 二、开发准备
利用上面的命令获取本次实验需要使用的所有素材

## 四、项目文件结构
【针对具有多个文件的项目或者文件之间彼此有依赖关系，若项目仅一个代码文件的可忽略此项】
【整个项目所有文件（依赖文件、代码文件等）的目录结构】
【本实验涉及到的文件（需修改、重新编写等）单独标出】

## 五、实验步骤
**(注意：本项目主要为了演示Web基本技术，对于安全性考虑不足，可能存在XSS和CSRF等漏洞，切勿直接用于生产环境)**
### 1. 设置背景
我们对于body添加以下CSS:
```CSS
background-image: url(background.jpg);background-size:100%;
```

然后将clone下来仓库中的background.jpg复制到你的目录，这是我在网上找的**可商用×*的图片，为了适应屏幕，经过了简单的比例裁剪。大家喜欢的话可以替换成自己的图片或者允许用户自定义。
（该图片由<a href="https://pixabay.com/zh/users/natassa64-7932121/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=3204824">natassa64</a>在<a href="https://pixabay.com/zh/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=3204824">Pixabay</a>上发布）

虽然没有做自适应的布局，图片在某些特殊屏幕上显示会不符合预期，但大部分情况下都是可以使用的。
### 2. 构建任务栏
首先我们先创建一个标准的HTML5文件
```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>WEB DESKTOP</title>
    </head>
    <body>
        
    </body>
</html>
```

然后再创建一个```style```标签，输入以下CSS
```CSS
.panel {
    left: 0px;
    position: absolute; /* 设置绝对位置 */
    bottom: 0px;
    width: 100%;
    vertical-align: bottom; /* 固定到底部 */
    background-color: gray;
    height:6%； /* 面板高度，可自行调整 */
    opacity:0.4; /*透明度*/
}
```

再在body中创建一个DIV,作为底部栏
```html
<div id="panel" class="panel"></div>
```

然后来创建“开始”菜单按钮

在panel的div中插入图标，我这里给大家提供了阿里巴巴图标库的一个PNG文件，大家可以自行替换
（我曾想使用svg，但发现排版有问题，所以才使用png)

```html
<img src="menu.png" id="button" style="max-height: 100%" />```

然后添加一段js来实现点击时的简单颜色变化相应
```html
    <script>
        document.getElementById("button").onmousedown = function() {
            document.getElementById("button").setAttribute("style", "max-height: 100%;background-color:darkgray ")
        }
        document.getElementById("button").onmouseup = function() {
            document.getElementById("button").setAttribute("style", "max-height: 100%;background-color: #grey")
        }
    </script>
```

### 3. 制作“开始菜单”面板
这一步相对比较复杂，我们来使用一个UI库，叫[layer](https://layer.layui.com/),这是一个包含在layui中的弹出层模块，在后面的窗口制作中我们也会用到它。
首先根据文档引入相关文件
```html
<script src="layui/layer.js"></script>
<script>
    layui.use('layer', function () {
        layer = layui.layer;
    });
</script>
```

然后根据文档使用我们的iframe层
```js
document.getElementById("button").onclick = function() {
    layer.open({
        type: 2,
        title: false,
        closeBtn: 0, //不显示关闭按钮
        shade: [0],
        area: ['340px', '215px'],
        offset: 'rb', //右下角弹出
        anim: 2,
        content: ['test/guodu.html', 'no'], //iframe的url，no代表不显示滚动条
    });
}
```


## 六、实验总结
【对该实验进行总结】

## 七、课后习题
尝试对代码的运行速度再进行优化，可以向我的git仓库（上面clone下来那个）提交PR

## 八、参考链接

