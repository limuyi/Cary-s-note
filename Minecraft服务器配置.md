# 前期准备

## 更新软件源
```
yum update
```
## 安装java
```
yum install java
```
## 安装screen
```
yum install screen
```

# 开始配置

## 开启一个新的screen会话
```
screen -S Minecraft # -S 是为会话取个名字
```
终端会被清空，但是已经在会话中了

screen 可能用到的命令会列在文末
## 创建目录
位置可自行选择
```
mkdir minecraft
cd minecraft
mkdir server  # 把server相关东西都放进去
cd server
```
## 下载minecraft的server文件
可以去 https://minecraft.net/download 找最新版本

wget命令下载慢的话可先下载到本地再用rz命令上传
```
wget https://s3.amazonaws.com/Minecraft.Download/versions/1.12.2/minecraft_server.1.12.2.jar
```
## 修改eula.txt文件
将eula=false改为eula=true
如server下没有该文件可先执行一遍启动文件命令
```
nano eula.txt
//文本编辑器可自行选择这里使用的是nano
//没有nano可使用vi文本编辑器，或者yum install nano下载
//nano 退出保存流程 Ctrl+x退出 -> 键入y确定 -> 回车
```
## 修改server.properties
把mode-online=true 改为 mode-online=false

## 启动文件
```
java -Xmx1024M -Xms1024M -jar minecraft_server.1.12.2.jar nogui
```
Should you want to start the server with it's graphical user interface you can leave out the "nogui" part.
本服务器没有图形化界面所以命令末添加 nogui 不需要gui界面
## 默认端口
默认端口为25565，即服务器地址为serer ip/25565

修改地址为server.properties中的server-port项
## 防火墙配置
如不能访问服务器请检查防火墙配置

这里是centos7 firewall配置

其他防火墙配置可自行百度“如何添加端口到防火墙”
```
# 添加25565端口
firewall-cmd --zone=public --add-port=25565/tcp --permanent
# 重启防火墙
systemctl restart firewalld.service
```
如不能访问请检查阿里云安全组是否添加25565端口
## 编写start.sh脚本
在server文件夹下新建start.sh

```
nano start.sh
```
添加以下语句
```
#!/bin/bash
java -Xmx1024M -Xms1024M -jar minecraft_server.1.12.2.jar nogui
```

# 启动流程

## 第一次启动
1.新建screen
```
screen -S Minecraft
```
2.打开server文件夹
```
cd usr/games/minecraft/server
```
3.启动服务器
启动脚本
```
./start.sh

```
 直接输命令
```
java -Xmx1024M -Xms1024M -jar minecraft_server.1.12.2.jar nogui
```

## 重新进入服务器
如果服务器已启动，或者关闭了但是没有退出Minecraft这个会画

1.检查当前按会话，查看Minecraft的话还存不存在
```
screen -ls
```
2.进入该会话
```
screen -r Minecraft
```
此时就恢复了退出前的状态

3.若没有查询到会话请按第一次启动方法重新新建会话并启动服务
# 附录

## screen常用命令
```
# 新建一个叫yourname的session
screen -S yourname
# 列出当前所有的session
screen -ls（或者screen -list）
# 回到yourname这个session
screen -r yourname 
# 结束当前session
exit 
```
## 举例
在minecraft会话中启动服务

断开链接

重新链接后显示的就是默认界面,可以进行其他操作

恢复到minecraft会话界面
```
screen -r minecraft
```
