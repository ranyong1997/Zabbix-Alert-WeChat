# Zabbix-Alert-WeChat zabbix 微信 等各类告警脚本

## 作者:火星小刘 邮箱:xtlyk@126.com   

## 关注作者B站，一起学习运维开发 https://space.bilibili.com/439068477

<a href="https://space.bilibili.com/439068477" target="_blank"><img src="https://github.com/X-Mars/Zabbix-Alert-WeChat/blob/master/images/5.jpg?raw=true" alt="B站火星小刘" width="50%" height="50%"></a>

### 包含脚本
1. 企业微信应用消息脚本 **wechat.py**
2. 企业微信群机器人脚本 **wechat-robot.py**
3. 钉钉机器人脚本 **dingtalk-robot.py**
4. 飞书机器人脚本 **feishu-robot.py**
5. 企业微信应用消息python2版本脚本 **wechat-py2-old.py**

### 交流群
<img src="https://github.com/X-Mars/Zabbix-Alert-WeChat/blob/master/images/1.jpg?raw=true" width="25%" height="25%"><img src="https://github.com/X-Mars/Zabbix-Alert-WeChat/blob/master/images/3.jpg?raw=true" width="46%" height="46%">

## **https://www.zabbix.com/cn/integrations/wechat** 本项目zabbix官方推荐位列第一，值得信赖
<img src="https://github.com/X-Mars/Zabbix-Alert-WeChat/blob/master/images/4.png?raw=true">

### 2023-09-08 更新
1. 添加钉钉机器人支持 **dingtalk-robot.py**
<img src="https://github.com/X-Mars/Zabbix-Alert-WeChat/blob/master/images/6.png?raw=true" width="70%" height="70%">
<img src="https://github.com/X-Mars/Zabbix-Alert-WeChat/blob/master/images/7.png?raw=true" width="80%" height="80%">

2. 添加飞书机器人支持 **feishu-robot.py**
<img src="https://github.com/X-Mars/Zabbix-Alert-WeChat/blob/master/images/8.png?raw=true" width="80%" height="80%">

### 2023-09-05 重要更新
1. 添加同时兼容 python2 与 python3 的告警脚本 **wechat.py**
2. 原有python2 告警脚本 重命名为 **wechat-py2-old.py**

### 企业微信群机器人脚本 wechat-robot.py

<img src="https://github.com/X-Mars/Zabbix-Alert-WeChat/blob/master/images/2.png?raw=true" width="90%" height="90%">

### 企业微信应用消息脚本 wechat.py
### 2018-10-13
1. 添加token缓存支持：避免频繁获取token 进而导致接口被限制
2. token过期，脚本将重新获取token，并再次执行之前发送操作

### 2018-07-09
**如何将报警同时发送给多个用户**
1. 企业微信支持3种发送方式：**针对用户发送（需要用户在企业微信中的id）**、**针对部门发送（需要部门id）**、**针对标签发送（需要标签id，通讯里---标签）**   
2. 对应去掉下图的注释即可
![群发设置](https://image.ibb.co/bTX3Go/20180709220015.png)

### 2017-11-23
**转载必须注明本项目地址**   
**https://github.com/X-Mars/Zabbix-Alert-WeChat**
**本脚本的出现离不开广大zabbix用户，大家可以免费试用，但不要用来盈利**

### 2017-08-08
1. 全部重写，代码更简洁易读
2. 舍弃原有**simplejson**，使用**requests**模块
3. 支持**python2**

### 需要具备一下条件  
 * 注册微信企业号（团队类型） [点击注册](https://qy.weixin.qq.com/)   或    注册企业号微信  [点击注册](https://work.weixin.qq.com/）
 * 近期腾讯把**微信企业号**升级为了**企业微信**，本脚本完全兼容。
#### 安装组件
1. 安装方法一
```shell
pip install requests
pip install --upgrade requests
```
2. 安装方法二
```shell
wget https://pypi.python.org/packages/c3/38/d95ddb6cc8558930600be088e174a2152261a1e0708a18bf91b5b8c90b22/requests-2.18.3.tar.gz
tar zxvf requests-2.18.3.tar.gz
cd requests-2.18.3
python setup.py build
python setup.py install
```
  
#### 下载安装脚本  
```bash  
git clone https://github.com/X-Mars/Zabbix-Alert-WeChat.git  
cp Zabbix-Alert-WeChat/wechat.py /etc/zabbix/alertscripts  
chmod +x /etc/zabbix/alertscripts/wechat.py  
```
  
### 企业微信设置  
#### 通讯录设置  
登陆企业微信控制台  
点击顶部 **通讯录** 添加子部门（运维部），并添加用户  
点击（运维部）后方的三个竖行圆点，记录 **部门ID**  
  
#### 创建应用  
点击顶部 **应用中心**，创建应用，应用名称为 **zabbix报警**   
**可见范围**，添加刚刚新建的子部门（运维部）  
点击 **zabbix报警**，记录 **AgentId**、**Secret**  
  
#### 应用权限设置  
点击顶部 **我的企业**，权限管理，新建普通管理组，名称填写 **zabbix报警组**  
点击修改 **通讯录权限**，勾选（技术部）后方的管理  
点击修改 **应用权限**，勾选刚刚创建的 **zabbix报警**   
点击刚刚创建的 **zabbix报警组**，记录左侧的 **CorpID 与 Secret**  
  
#### 收集企业微信相关信息
1. 记录 **应用ID**
2. 记录 **CorpID 与 Secret**
3. 记录 **子部门（运维部）ID**
  
  
### zabbix设置
1. 添加示警媒介  
#### 管理-->示警媒介  
名称填写 **微信报警**，类型选择 **脚本**，脚本名称填写 **wechat.py**（Python3 使用 wechat-py3.py）  
#### 管理-->用户-->示警媒介  
类型选择 **微信报警**，收件人添加 **微信企业号通讯录内的，用户帐号**

完成


License
---
[996ICU License](LICENSE)  
