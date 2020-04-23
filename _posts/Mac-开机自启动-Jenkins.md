---
title: Mac 开机自启动 Jenkins
date: 2020-04-23 11:10:48
tags: [Mac,Mac 开机自启动,Jenkins]
categories: [Mac,Jenkins]
---



### 下载 Jenkins

[Jenkins](https://jenkins.io/) https://jenkins.io/

下载 `war` 安装包 版本号 `2.22.1` 下载连接 [Jenkins.war](http://ftp.yz.yamagata-u.ac.jp/pub/misc/jenkins/war-stable/2.222.1/jenkins.war) 重命名 为**jenkins_2.222.1.war**

存放路径 **~/Dev/bin/jenkins/jenkins_2.222.1.war**

### 启动脚本

#### 脚本内容

**~/Dev/bin/jenkins/startupJenkins.sh**

```
port=8080
#根据端口号查询对应的pid
pid=$(netstat -anvp tcp  | grep $port | awk '{print $9}' | awk -F"/" '{ print $1 }');

#杀掉对应的进程，如果pid不存在，则不执行
if [  -n  "$pid"  ];  then
    echo "查询到占用端口号:$port 的应用PID: $pid ";
    kill  -9  $pid;
fi

echo "Jenkins Start ... "
nohup java -jar ~/Dev/bin/jenkins/jenkins_2.222.1.war  > /dev/null 2>&1 &
```



#### 脚本添加权限

`chmod 777 startupJenkins.sh`

#### 修改 startupJenkins.sh  文件的打开方式

右击 -> 打开方式 -> 其他 -> 实用工具 -> 终端

![mac_jenkins_auto_start](mac_jenkins_auto_start.jpg)



### 添加开机启动项

偏好设置 -> 用户与群组 -> 登录项 -> 添加 -> 选择 **startupJenkins.sh**

![mac_jenkins_auto_cmd_add](mac_jenkins_auto_cmd_add.jpg)



### 重启 Mac 测试
浏览器打开 http://127.0.0.1:8080

![mac_jenkins_auto_start_success](mac_jenkins_auto_start_success.jpg)