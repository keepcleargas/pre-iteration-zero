## 工程实践

在ThoughtWorks，几乎每个团队都在遵循着某些敏捷实践，但是每个团队的实践都有不同。敏捷本身的意义就是拥抱变化，持续改进。我怀疑，即使最开始所有团队都学习了同样的实践，经过几个迭代之后，每个团队都会演化出适合自己团队`节奏`的实践集。

我对一些同事做过采访，每个被采访者只需要回答一个问题：

>假设需要你启动一个项目，项目成员已经就绪，唯一的问题是，客户对敏捷实践抱有怀疑（他已经被市面上的各种`敏捷`吓坏了），因此他不太支持那些`新鲜的`，`反直觉`的敏捷实践。你推行的所有实践都可能会遇到挑战，另外由于有交付压力，你不得不做出一些妥协。
>那么，你接受的最低限度的敏捷实践的集合是什么？（也就是说，如果客户和你无法在这个集合上达成一致的话，那么你就会退出该项目）

整理后的一个列表是这样的：

-  可视化的需求卡片墙
-  迭代方式管理
-  持续集成（编译，检查，测试，打包）
-  测试覆盖全面
-  每日站会
-  回顾会议
-  知识传递（结对编程，Git Pull Request，Code Review）
-  版本控制
-  自动化脚本（构建，部署）

### 版本控制系统

我在2012年的时候，还听说有客户使用基于ftp的源码控制，也就是说本地开发完成之后，通过ftp拷贝到远程服务器并覆盖的方式。这个现象可能现在已经不存在了，我参加过的大部分项目都采用了某种形式的版本控制，很多比较传统的企业会采用`subversion`，而大多数较新的项目都采用了`git`作为版本控制系统。

版本控制系统不但可以帮你将改动痕迹保存起来，还可以很方便的提供`diff`功能，这样你可以和其他人讨论修改内容（后边的Code Review小节我们会详细讨论）。另外，版本控制系统（如git）可以让你回退到历史的某个版本，这样你可以很容易的构建出当时的包并进行测试，这在查找到底是哪次提交引入了缺陷时非常重要（git提供`bisect`字命令，可以更加迅速的定位缺陷引入时的版本）。

无论如何，版本控制系统已经成为开发的标配，我们推荐你使用功能强大的`git`，它提供的丰富特性更适合分布式团队的协作。

### 迭代开发

闭门造车的时代已经一去不复返了。需求分析3个月，开发半年，测试半年的瀑布方式也与飞速发展的时代不匹配了。快速，轻量级的开发，发布，测试已经成为常态，没有人愿意为软件的某个功能而等上好几个月。

### 持续集成

### 自动化测试

### 站会

### 回顾会议

### 知识传递

在ThoughtWorks我们如何做培训

### 自动化一切