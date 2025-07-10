# ECNU_NETWORK_LOGIN

华师大上网验证客户端，原始代码由[ECNUSR](https://github.com/ECNUSR/ecnu_network_login)编写，在使用过程中发现了一些坑，解决记录如下：

# Preparation
1. clone source
```
git clone git@github.com:Skylyong/ECNU_NETWORK_LOGIN.git
```

2. Install dependencies:

切换到项目目录(setup.py所在的目录),执行下面的命令安装并在命令行注册`ecnu_net_login`命令（这里通过源码的方式进行安装，方便以后认证方式变化，通过改变源码进行适配）
```
pip install .
```

# Usage

```bash
# 帮助文档，ecnu_net_login和ecnu_network_login均能识别
ecnu_net_login --help
ecnu_network_login --help

# 登录（循环登录）
ecnu_net_login -u {{学号}}
ecnu_net_login -u {{学号}} -m LOOP

# 登录（仅一次）
ecnu_net_login -u {{学号}} -m ONCE

# 远程获取登录URL（如果远程服务器没网，没法安装此包，可以在有校园网环境的机器上远程支持获取URL，然后在服务器上wget该URL）
ecnu_net_login -u {{学号}} --ip {{服务器IP}} -m PRINT
```
# Notice

需要联网的主机事先不能设置任何代理上网，如果设置了代理上网，则会**报错**。
请先使用下面的命令，查看是否设置了代理上网
```
echo $http_proxy
echo $https_proxy
echo $HTTP_PROXY
echo $HTTPS_PROXY
echo $all_proxy

```
   如果设置了某一项代理上网，请使用下面对应的命令取消代理
```
unset http_proxy
unset https_proxy
unset HTTP_PROXY
unset HTTPS_PROXY
unset all_proxy
```

取消代理上网后，执行命令`ecnu_net_login -u {{学号}} -v DEBUG`,并按照提示输入密码，出现如下的提示，则说明网络登录成功。
```bash
2025-07-10 14:24:55,094 DEBUG: 网络在线~~无需重新登录~~
2025-07-10 14:25:55,363 DEBUG: 网络在线~~无需重新登录~~
2025-07-10 14:26:55,621 DEBUG: 网络在线~~无需重新登录~~
2025-07-10 14:27:56,099 DEBUG: 网络在线~~无需重新登录~~
2025-07-10 14:28:56,311 DEBUG: 网络在线~~无需重新登录~~

```
如果主机没法上网，不能下载依赖包，原作者提供了`远程登录`选项。我这里先使用代理上网搞定了安装依赖，再根据上面的设置取消代理，因此，这里没有对该功能做测试。
