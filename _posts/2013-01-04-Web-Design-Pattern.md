---
published: true
layout: post
title: "Web Design Pattern&#58; Responsive Table for Mobile &amp; Desktop Web"
categories: 
  - announcement
  - blog
tags: 
  - trantect
  - github

---

最近做的一个 Web App，整体框架是基于Bootstrap，需要支持包括桌面、平板设备和手机等多种尺寸的浏览器。Bootstrap 是由Twitter推出的一个非常受欢迎的、灵活的及开源的用于前端开发的工具包。现在，越来越多的移动设备充斥市场，改变了人们使用互联网的方式，重要的是基于Bootstrap的精美网页也在不断增长 ，仅仅只追求桌面的美观是远远不够的，要时刻关照小型移动设备用户的视觉感受。

**Pattern: ** 移动和桌面Web响应式表格设计

**Issue: ** 改善在小型移动设备上的 Web App 中的表格使用体验，使用同一套 HTML 和 CSS 支持从桌面设备到手持终端等多种尺寸的浏览器，保持一致的风格而又能够根据设备情况调节部分元素的展现形式。

![Alt text](/assets/themes/twitter/bootstrap/img/pattern1.jpg)

上图中，整个页面使用了 Bootstrap 。其内容以表格为主，这与以文字为主的网页大不相同。页面变窄时，表格的布局仍然被保持，需要在一行中显示多栏信息。此时可能造成上图中的文字折行或需要左右滚动屏幕。这会让用户使用起来很不方便。（在测试过程中，通过缩小浏览器的宽度检查在不同设备上的效果。）需要有一种手段可以在较窄的屏幕上自动调整表格布局，如减少列数或将同一条记录的多栏信息多行显示。

**Solution: ** ***Responsive Design***（响应式设计）中 Medias Query可根据设备和分辨率的不同而使用不同的样式。

Bootstrap 中已包括了一些 responsive design ，如 grid 系统和 nav-bar 等。（这里有给出Bootstrap的官网，[http://twitter.github.com/bootstrap/](http://twitter.github.com/bootstrap/) 

![Alt text](/assets/themes/twitter/bootstrap/img/pattern2.jpg)

如下图中，Trantect 公司网页效果中的 nav-bar:

![Alt text](/assets/themes/twitter/bootstrap/img/pattern3.jpg)

但表格的 Responsive Design 需要一点额外的工作。

![Alt text](/assets/themes/twitter/bootstrap/img/pattern4.jpg)

通过修改 HTML 和 CSS 解决手持终端等多种尺寸的浏览器问题，如下图：

![Alt text](/assets/themes/twitter/bootstrap/img/pattern5.jpg)

上图中，页面变窄时，表格的布局被切换成一列中显示多行信息，方便用户进行操作。具体内容参考：
[http://elvery.net/demo/responsive-tables/](http://elvery.net/demo/responsive-tables/)

**Consequences: ** Web App 中的响应式表单设计

![Alt text](/assets/themes/twitter/bootstrap/img/pattern6.jpg)

这样改善了小型移动设备上的 Web App 中的表格使用体验。


**Conclusion：** 响应性的Web设计终将成为一种趋势，但响应性的Web设计是如此的远不止一个趋势，它是一种新的思维方式。
在一个多设备的世界，上网本似乎是随处可见，响应性的Web设计给人的感觉更像是一个才刚刚开始展现其潜在能量自然的过程。
