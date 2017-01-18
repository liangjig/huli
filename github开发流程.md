##github 开发流程
###为什么？为了满足什么？
* 多项目并行开发
* 集成slack、fabric等
* 分支开发,fork至个人目录,PR后合并master

### 参考资料
> [Git 工作流程](http://www.ruanyifeng.com/blog/2015/12/git-workflow.html)

> [团队合作流程](http://book.haoduoshipin.com/gitbeijing/github_flow.html)

> [Github 开发流程入门【老崔wiki】](http://wiki.zplay.cn/pages/viewpage.action?pageId=23277862)

###分支规范
####分类
* master 主干,永久且只有1个,一直都是最新的线上代码,发布线上代码使用
* develop-* 开发分支,多个,依照项目而定
* feature-* 功能分支,多个,来自develop,功能的拆解,各自开发人员的任务
* fixbug-* 紧急修复bug分支,来自master,0个或1个

**master**：最终合并，发布线上代码使用
**其它分支**：部署测试环境

###命名
* develop-* 星号为项目名称和加额外信息,附加信息可以是日期或是项目版本等.
```
    
    1   develop-optimization-20151224
    
 2   develop-optimization-v2
```
* feature-* 星号建议包含项目+姓名为前缀,因为是个人开发分支,自己分清即可
```
    
    1   feature-optimization-sunhuai
    
 2   feature-optimization-liangji
```

* fixbug-* 建议包括修复bug描述星号为数字，fix版本号从1开始，例如key管理
```
    
    1   fixbug-keymanage-1
    
 2   fixbug-keymanage-2
```
###操作示例
#### 配置github帐号 ssh keys

1、生成密钥

windows:可以在git bash中，默认生成目录为C:\Users\用户目录\.ssh

linux:默认生成目录为~/.ssh/

```
ssh-keygen -t rsa -C "your email"

```
按3个回车，密码为空这里一般不使用密钥。

最后得到了两个文件：id_rsa和id_rsa.pub

2、在github上添加ssh密钥，这要添加的是“id_rsa.pub”里面的公钥
将id_rsa.pub中的内容复制出来
打开个人Settings-->SSH keys-->Add SSH key

Title 随便写（或者标记一下，例如是公司开发机上的）

Key 粘贴之前复制的内容

点击 “Add SSH key”

这样SSH key就添加的Github,此时刚添加的前面小钥匙是灰色的

3、检测SSH key
输入命令
```
ssh git@github.com

```

此时会验证SSH key是否可以访问Gitbub

成功显示如下：
> 

    Hi your_name! You've successfully authenticated, but GitHub does not provide shell access.

    Connection to github.com closed.

刷新下github页面，此时刚添加的前面小钥匙是绿色的

###开发(develop)流程
1、 通常功能开发时间较长，甚至多人合作开发，以key管理(managementPlatform)为例,liangji和sunhuai共同开发

2、 先从yumimobi/master拉出一个yumimobi/develop-keymanage-v1

3、 liangji从分支 yumimobi/develop-keymanage-v1 fork到自己个人帐户下

4、 获取个人项目clone地址

5、 在命令行（或者windows git bash）执行git clone [项目地址] 的方式, 将项目clone

```
git clone git@github.com:xxxx/managementPlatform.git

```
6、 然后进入该目录下, 创建新分支。 用git checkout -b 新分支名称  的方式创建。 

```
cd develop-keymanage-v1
git checkout -b develop-keymanage-v1

```

7、 开始开发 

8、 开发完成后git add 添加、git commit提交

9、将commit后的分支push到自己个个人账号下的项目（可用sourcetree或命令行git push）

```
git push origin develop-keymanage-v1

```
10、然后访问公司账号下的该项目页面，如果有新推送提示，可直接点击右侧按钮创建pull request， 否则手动点击New pull request 按钮，在此的对比应该是

**base:fork** yumimobi/managementPlatform **base**:develop-keymanage-v1 ... **head fork**:liangji/managementPlatform **compare**:develop-keymanage-v1

在Reviewers里可以指定代码审核人可以使用@,例如@sunhuai

10、 sunhuai收到后，确认没问题，点击**“Merge pull request”**


###增加小功能(feature)流程

###修复bug（fixbug）流程