## Maven Release Plugin 介绍
> 使用maven进行模块化开发，依赖管理，并使用git进行版本控制时，如何进行版本迭代。

### 版本号说明
> 开发中务必使用如下约束进行版本迭代，并更新版本号，

我们在开发的过程中，下载jar包的时候经常会发现某个jar类似这样：1.2.3-beat-4.jar
多么复杂的一个名称。。。下面来解释一下，这里每个数字的含义：
“ 1 ” :  表示该版本的第一个重大版本
“ 2 ” :  表示这是基于重大版本的第二个次要版本
“ 3 ” :  表示该次要版本的第三个增量
" beat-4" : 表示该增量的一个里程碑
用一个图来描述：
< 主版本 >  ------   < 次版本 > ------ < 增量版本 > ------ < 里程碑版本 >

* 主版本：表示了项目的重大架构变更  struts1 --  struts2
* 次版本：表示较大范围的功能增加和变化  Nexus1.5 ----   Nexus1.4
* 增量版本：一般表示重大Bug修复  
* 里程碑版本：指某一个版本的里程碑   \*.\*-alpha-1  \*.\*-beat-1

看起来有点麻烦啊， 但是在一般来说，我们只会声明主版本和次版本，增量版本和里程碑版本就不一定了。
注：maven中约定的版本次序：
对于主版本、次版本、增量版本来说他们的比较是基于数字的，因此：1.5>1.4>1.3>1.2.11>1.2.8
对于里程碑版本来说，比较是基于字符串的，因此：1.5>1.4>1.3>1.2.3>1.2.11

### 主干、分支、标签

上面的笔记中提到了主干和标签，到底如何理解主干、分支、标签呢？

* 主干: 项目开发代码的主体，是从项目开始到当前都处于活动的状态，从这里可以获得项目最新的源代码(可用的)和几乎所有的变更历史
* 分支: 从主干的某个点分离出来的代码拷贝，通常可以在不影响主干的前提下，在这里进行重大的bug修复或者实验性质的开发，如果达到了预期的目的，通常将这里的变更合并到主干中去。
* 标签: 用来标识主干或者分支的某个点的状态，以代表项目的某个稳定状态，也就是通常说的发布状态

这三个元素，可以清晰的描述出项目的版本管理，而且也已经成了一个默认的行业标准。

### 自动化版本发布
> 使用 [maven-release-plugin](https://maven.apache.org/maven-release/maven-release-plugin/examples/prepare-release.html)，
相关参考博客：[Maven自动化部署](http://www.yiibai.com/maven/maven_deployment_automation.html)、[Maven release for Git](http://blog.sina.com.cn/s/blog_507c71550100ojif.html)、[Maven详解之------maven版本管理](http://blog.csdn.net/wanghantong/article/details/38424065)
代码提交主要有一下步骤：
1. Prepare a Release
2. Rollback a Release
3. Perform a Release

#### Prepare a Release [原文](https://maven.apache.org/maven-release/maven-release-plugin/examples/prepare-release.html)

Prepare a Release需要进行如下检测：

1. 检查项目是否有未提交的代码
2. 检查项目是否有快照版本依赖
3. 根据用户的输入将快照版本升级为发布版
4. 将POM中的SCM信息更新为标签地址
5. 基于修改后的POM执行maven构建
6. 提交POM变更
7. 基于用户输入为代码打标签
8. 将代码从发布版升级为新的快照版
9. 提交POM变更

执行代码：
```
 mvn release:prepare
```
执行出错后重新执行可以执行如下代码中的一条
```
mvn release:prepare -Dresume=false
mvn release:clean release:prepare
```
执行过程中，文件本修改，希望回滚，则可以使用 **release:rollback** 实现该功能

##### 多模块项目
如果项目中有多个模块，可以通过设置**autoVersionSubmodules** 为 **true**，只需要修改一次release version即可。

#### Perform a Release 执行release
执行Release操作需要两个阶段

1. 检查SCM地址
2. 执行预先定义的Maven目标发布项目，（默认为deploy site-deploy）

```
mvn release:perform
```


#### Create a Branch
```
mvn release:branch -DbranchName=my-branch
```