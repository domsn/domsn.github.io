title: 扔掉你的SSH工具吧
date: 2015-06-05 17:26:31
tags:
- ssh
- ssh-keygen
- ssh-copy-id
categories: 
- LEVEL UP
---
#### 故事背景
*如果你存在下面的情况，我想你可以继续看下去！*
> * 你还在使用各种各样的SSH工具，来连接服务器？
> * 系统重装/迁移环境/工具更换，需要各种备份/导入/导出？
> * 更换环境的时候，会不会为每个服务器的配置所烦恼？
> * 这样不够Cool!


#### 系统要求
	OS X / Linux, 本人使用的环境是OS X。


#### 配置服务器
编辑SSH配置文件

```bash
$ vi ~/.ssh/config
```

添加服务器信息，常用属性如下：

- Host 服务器的别名，便于SSH连接，可根据实际情况命名
- HostName 服务器的域名/IP地址
- Port 端口（可选），如果是默认端口可不填
- User SSH连接的用户

下面举两个例子,每个例子为一个服务器的配置（间隔使用空行）：

```bash
#我的服务器
Host mine
HostName xifan.me
Port 12345
User xifan

#公司测试服务器
Host c.t
HostName 172.42.23.177
Port 22222
User root
```

#### 连接服务器

打开你的Terminal，连接我的服务器
```bash
$ ssh mine
```

连接公司测试服务器
```bash
$ ssh c.t
```
根据提示输入服务器密码，即可登陆成功。
合理命名服务器，带着你的配置文件，说走就走，So Cool！

#### 免密码登陆

> 虽然上面很Cool，但我想说，其实可以更Cool！
> 每次都要手动输入密码，是的，不够Cool！

使用ssh-keygen生成密钥，一路回车，全部使用默认值，会生成一个公匙(~/.ssh/id_rsa.pub)和私匙(~/.ssh/id_rsa)。
```bash
$ ssh-keygen -t rsa 
```
使用ssh-copy-id把你的公匙复制到对应的服务器，这样就可以免密码登陆了。

> 如果你用Linux，那么恭喜你，你应该可以直接用。
> 如果你用OS X，那您还需要安装`brew install ssh-copy-id`，但如果你连brew都还没安装，那请你参考 [brew.sh](http://brew.sh/ "Homwbrew")，只能帮到你这里了。

复制公匙到我的服务器，根据提示输入密码
```bash
#参数p,代表端口(可选)
$ ssh-copy-id -p 12345 xifan.me
```
再此尝试登陆我的服务器
```bash
$ ssh xifan
```
**不用密码，So Cool！**
**带上你的配置文件和公匙私匙！**
**走到哪都可以很方便的免密码登陆服务器！**


#### 番外篇
> \>> ssh-copy-id 到底干了什么？
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;他就是把你的公匙内容追加到服务器的这个文件末尾 ~/.ssh/authorized_keys
> \>> ~/.ssh/authorized_keys 又有啥作用？
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;存放允许登陆的公匙

  
  
  
**Mission Completed!**
**(END)**
