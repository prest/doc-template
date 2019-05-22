---
title: "贡献合作"
date: 2017-08-30T19:07:12-03:00
weight: 16
menu: main
---

您是否发现了错误或想要推荐新功能？ 我愿意接受反馈。 请打开一个新的 [issue](https://github.com/prest/prest/issues) 让我知道你的想法.

也欢迎提交 [pull requests](https://github.com/prest/prest/pulls).

## 运行测试

克隆存储库并创建测试数据库并插入规范的虚拟数据。

```
PREST_PG_HOST=127.0.0.1 PREST_PG_DATABASE=prest sh ./testdata/schema.sh
```

在测试数据库上运行迁移。

```
PREST_PG_HOST=127.0.0.1 PREST_PG_DATABASE=prest sh ./testdata/migrations_test.sh
```

运行测试

```
PREST_PG_HOST=127.0.0.1 PREST_PG_DATABASE=prest sh ./testdata/test.sh
```

# 贡献指南

## 介绍

本文档介绍了如何为pREST项目提供更新。 .

## Bug 报告

请使用各种关键字搜索问题跟踪器上的问题，以确保您的错误尚未报告。

如果不存在, 打开一个[issue](https://github.com/prest/prest/issues/new) 并回答问题，以便我们能够理解并重现有问题的行为。

为了展示您所遇到的问题是pREST本身的问题，请写些清楚、简洁的说明，以便我们可以重现（即使它看起来很明显）。 您越详细和具体，我们就能越快解决问题。查看 [如果有效的报告Bugs](http://www.chiark.greenend.org.uk/~sgtatham/bugs.html).

请善待我们，请记住pREST坚持不懈地为您服务，并且您会获得免费帮助。

## 讨论你的设计

该项目欢迎提交，但如果您想要更改或添加内容到perst存储库，请让每个人都知道您正在做什么。

在开始为perst项目编写新内容之前，请 [提交问题](https://github.com/prest/prest/issues/new).

此过程使每个人都有机会验证设计，有助于防止重复工作，并确保该想法符合项目和工具的目标。 它还会在编写代码之前检查设计是否正确; 代码审查工具不是高级别讨论的场所。

## 测试 redux

在发送代码进行审核之前，请运行整个树的所有测试，以确保更改不会破坏其他用法并保持升级的兼容性。 为了确保您像我们一样运行测试套件，您应该安装 [Travis CI](https://travis-ci.org/), 因为我们正在使用服务器进行连续测试。

## 代码审查

pREST必须在接受变更之前对其进行审核，无论是谁进行更改，不管所有者或维护者。


请尝试让我们轻松查看您的拉取请求。 请阅读e "[How to get faster PR reviews](https://github.com/kubernetes/community/blob/master/contributors/devel/faster_reviews.md)" 指南, 它为您可能想贡献的任何项目提供了许多有用的提示。 一些关键点：

* 提出小拉请求。 越小，审查越快，很快就会合并。
* 请勿进行与PR无关的更改。也许在一些评论上有拼写错误，也许在一个函数上欢迎重构...但如果这与你的PR无关，请为此做另一个PR。
* 将大的PR请求拆分为多个小PR请求。 与巨大的PR相比，增量变化的审查速度更快。

## 签署你的工作

在补丁解释的最后，签名是一个简单的行。 您的签名证明您编写了补丁或以其他方式有权将其作为开源补丁传递。 规则非常简单：如果您可以认证[DCO]（DCO），那么您只需在每个git提交消息中添加一行：

```
Signed-off-by: Thiago Avelino <avelino@email.com>
```

请使用您的真实姓名，我们真的不喜欢假名或匿名捐款。我们在没有秘密的开源世界里。如果你设置`user.name`和`user.email`的 git configs，你可以使用`git commit -s`自动签名你的提交。

## 维护者

为了确保检查每个PR，我们有[团队维护者]（MAINTAINERS）。 每个PR **必须** 由至少两个维护者（或所有者）审核才能合并。 维护者应该是pREST的贡献者并且贡献了至少4个被接受的PR。 贡献者应该在 [Gitter develop channel](https://gitter.im/prest/prest)中作为维护者申请。 所有者或团队维护人员可以邀请贡献者。 维护者应该花一些时间进行代码审查。 如果维护者没有时间这样做，他们应该申请离开维护团队，将荣幸地成为**顾问团队的成员**。 当然，如果顾问有时间进行代码审查，我们很乐意欢迎他们回到维护团队。 如果维护者处于非活动状态超过3个月而忘记离开维护团队，则所有者可能会将他或她从维护团队转移到顾问团队。

## 拥有者

由于 pREST 是由社区维护的, [Nuveo](https://nuveo.com.br/en) (理想化的公司) 不提供专业支持，为了保持发展健康，我们每年将选出三个拥有者。 所有贡献者可投票选出最多三名候选人，其中一名将是主要所有人，另外两名是助理所有人。 当新拥有者当选后，老拥有者将放弃新当选拥有者的所有权。 如果拥有者无法这样做，其他拥有者将协助将所有权转让给新当选的拥有者。

选举结束后，新主人应主动同意 [CONTRIBUTING](CONTRIBUTING.md) 要求，位于 [Gitter main channel](https://gitter.im/prest/prest). 以下是要说的话:

```
我很荣幸当选为pREST的所有者，我同意 [CONTRIBUTING](CONTRIBUTING.md). 我将把部分时间花在坚持pREST 上，引领pREST的发展。
```

## 版本

pREST 将 `master` 分支作为 tip 分支并具有版本分支，例如`v0.1`。 `v0.1`是一个发布分支，我们将标记`v0.1.0`进行二进制下载。 如果`v0.1.0`有bug，我们将接受`v0.1`分支上的pull请求，并在将bug修复也引入master分支后发布`v0.1.1`标记。
由于`master`分支是tip版本，如果你想在生产中使用pREST，请下载最新的release标签版本。 所有分支都将通过GitHub进行保护，每个分支的所有PR必须由两个维护者进行审核，并且必须通过自动测试。


## 版权

您提供的代码应使用标准版权标题：

```
// Copyright 2017 The pREST Authors. All rights reserved.
// Use of this source code is governed by a MIT-style
// license that can be found in the LICENSE file.
```
存储库中的文件包含从添加到上次更改年份的年份的版权。 如果版权作者被更改，只需将标题粘贴在旧版本下方即可。

