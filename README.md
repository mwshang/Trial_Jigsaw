# Trial_Jigsaw

### 更新说明
- 2019-08-14: 创建本仓库
- 2019-11-30: 增加对注册页面的测试

### 介绍

仅限个人学习使用，不针对任何人或任何企业和组织。通过对比图像和图像识别等一些方式，去识别并跳过拖动验证的方法。

![](media/demo2.gif)

![](media/demo1.gif)

### 如何找到缺口？

主要就是都是针对网上的一些方法和思路的总结。然后根据实际的业务需求进行的调整。

网上有很多人都提供了一些其它平台（或者针对以前的方案），其中大多数是针对原图和缺口图同时存在的方案，这种一般都是采用对比图片的像素点，把最左侧的不一致点位标出来，来找到缺口的位置。

但是现在大多数的滑块验证，一般都不提供缺口了，基本都是提供一个原图作为背景，然后再提供一个滑块图片用于显示。

那么这里通过使用opencv的“模板匹配”的这种方式来实现，仅通过滑块和缺口图找到缺口位置的。

但是截至目前位置，这种识别一般情况只能针对每一家的不同情况，先处理图片才能得到好的效果。

当然还有一些大神，已经动用了机器学习去搞他们了。。。

其实针对jd，主要的难点是如何模拟人操作单动作轨迹，不让对方的机器学习发现。

### 相关的库

1. opencv-python
2. selenium
3. numpy
4. pillow

### 使用说明

1. 安装环境需要的库
2. 安装所需的webdriver（chrome、firefox等）
3. 在 /app.main.py 中有程序的入口

### 问题说明

##### 1. 实际拖拽操作的时候，发现滑动会出现卡顿的情况。

经过调查发现是每次执行的 `move_by_offset` 的方法时，会有一个停顿时间。

我的解决方法：需要修改selenium，源码中 `class PointerInput(InputDevice)` 的 `DEFAULT_MOVE_DURATION` 属性的值，从250调低，一般可能是10 - 70左右（具体需要测试）。（另外我的selenium是3.141.0版本，没有找到从外界传入或者修改该参数的位置，如果有知道可以告诉我一下，谢谢了）

相关文章：

[《使用Python Selenium 实现拖拽动作时动作不流畅》](https://blog.csdn.net/qq_36250766/article/details/100541705)