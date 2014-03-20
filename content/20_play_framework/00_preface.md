2014年3月12日是Web（万维网）诞生25周年的纪念日，现如今，你生活在“网络”的世界，没有Web怎么能行。

Web是网络的中核，几乎每门语言都能构建Web应用，专门为Web而生的PHP、ASP、JSP等就不必说了，这些技术都在很久远的年代就出现了，直到现在也都在现役中。后起之秀，比如Ruby on Rails（ http://rubyonrails.org/ ，简称Rails，2004年7月发布第一个版本）、Django（ https://www.djangoproject.com/ ，2005年11月16日发布0.90版 *注 1*）。现在，这两个Web框架几乎成了startup们制作原型、快速开发的不三之选。

Scala也不例外，Play Framework（*注 2*）就是这么一个框架。本章内容即将带你进入Play世界，一起Play！

首先，我们基于Play的官方文档，对Play的架构、使用方法等进行介绍。之后我们会使用Play来构建一个简单的Web应用，并部署到Heroku（*注 3*）上。


这部分内容主要包括：

- [Play简介](01_intro.md)
- [安装Play](02_install.md)
- [创建第一个Play应用](03_first_application.md)
- [Controller](04_framework_controller.md)
- [模板引擎](05_framework_template.md)
- [路由分发](06_framework_route.md)
- [使用数据库](07_databases.md)
- [异步处理](08_synchronous.md)
- [表单验证](09_form_and_validation.md)
- [部署Play应用](10_form_and_validation.md)
- [完整示例](11_project_fireup.md)


*注 1：<https://www.djangoproject.com/weblog/2005/nov/16/firstrelease/>*  
*注 2：<http://www.playframework.com/>*  
*注 3：<http://www.heroku.com/>，一个PasS平台，除了一个应用执行环境之外， 它还提供了很多组件，比如数据库、缓存、日志、监控、邮件等。你可以免费在heroku上免费运行一个dynos单元。*
