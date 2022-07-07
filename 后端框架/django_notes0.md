# Django 简介
Django 是一个高级的 Python 网络框架，可以快速开发安全和可维护的网站。
优点：
- 完备性
    功能完备，提供的基础功能多
- 通用性
    可以用于构建几乎任何类型的网站，与任何客户端框架一起工作
- 安全性
    提供自动保护网站框架避免安全错误功能
- 可拓展
    基于组建的“无共享”架构，架构之间相互独立
- 可维护性
    代码遵照设计原则和模式，使用不重复自己（DRY）原则避免不必要重复
- 灵活性
    Python支持多平台优势

Django提供了一组组件来处理大多数 Web 开发任务和一个（或两个）首选的使用方法。实现了特定框架和无限制框架的优点。

## Django 项目结构
Django 网络应用程序通常将处理每个步骤的代码分组到单独的文件中：
- URLs: URL 映射器用于根据请求 URL 将 HTTP 请求重定向到相应的视图。URL 映射器还可以匹配出现在 URL 中的字符串或数字的特定模式，并将其作为数据传递给视图功能。
    > 虽然可以通过单个功能来处理来自每个 URL 的请求，但是编写单独的视图函数来处理每个资源是更加可维护的。

- View:  视图 是一个请求处理函数，它接收 HTTP 请求并返回 HTTP 响应。视图通过模型访问满足请求所需的数据，并将响应的格式委托给  模板。
 
- Models:  模型 是定义应用程序数据结构的 Python 对象，并提供在数据库中管理（添加，修改，删除）和查询记录的机制。
 
- Templates: 模板 是定义文件（例如 HTML 页面）的结构或布局的文本文件，用于表示实际内容的占位符。一个视图可以使用 HTML 模板，从数据填充它动态地创建一个 HTML 页面模型。可以使用模板来定义任何类型的文件的结构; 它不一定是 HTML！

## Django 安装与创建项目
1. 安装python
    > 推荐使用python虚拟环境 如anaconda
    方便进行版本管理、环境配置
2. pip安装Django
    安装命令主要适用于windows：`pip3 install django`
3. 检验安装
    `python -m django --version`
    如果没有正确显示版本号需要重新进行第二布
4. 创建测试项目
    进入一个新建的文件夹（也可以不新建，即在当前路径上创建项目）
    `cd filepath` `mkdir new_filename`
    创建startproject（名字可以自定义）
    `django-admin startproject mytestsite`
    进入创建的项目路径下，使用命令运行
    `cd .\mytestsite\`
    `python manage.py runserver`
5. 出现“Starting development server at http://127.0.0.1:8000/ ”提示则运行成功
    访问ip可以查看已经启动的项目

## 项目实践学习
https://developer.mozilla.org/zh-CN/docs/learn/Server-side/Django/skeleton_website
MDN的本地图书馆项目










