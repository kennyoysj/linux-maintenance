## java
1. java环境的安装
由于webUpd8 team已经不在维护java8了，所以之前通过命令update apt库然后快速安装的方法已经不能用了
```
# this method is invalid
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
```
这里只能去ppa查找openjdk8的安装方案
* openjdk安装方案
找到[PPA for OpenJDK uploads (restricted)](https://launchpad.net/~openjdk-r/+archive/ubuntu/ppa)team
```
sudo add-apt-repository ppa:openjdk-r/ppa
sudo apt-get update
```
查找可以安装的版本，现在最高已经到13 java11为LTS长期支持版本
```
apt search openjdk*
# 第一个命令可能搜索不到什么东西这时可以用apt-cache命令然后根据需要安装即可
apt-cache search openjdk*
```
