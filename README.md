# vernemq - plugs

本项目为vernemq 拓展插件 利用httpAPI + js 开发 无侵入性,把代码放入项目对应路径即可，本插件仅作学习研究



## 背景：

VerneMQ 是一个高性能、分布式的 MQTT 消息代理。可在流行的硬件上轻松实现水平和垂直扩展，用于支持高并发的消息发布和订阅服务，同时维持低延迟和容错特性。

MQTT 是一个开放的工业标准，是一个轻量级的基于发布订阅模型的消息协议，特别适合用于一些非可靠网络环境下的小型和嵌入式设备使用。VernelMQ 实现了 MQTT 3.1 和 3.1.1 规范。		

官方API:https://docs.vernemq.com/administration/http-administration



最近学习vernemq  ， 感觉没有监控页面，用起来不是很爽， 自己利用 Vmq 的HTTPAPI 开发一个页面。

## 效果展示：

#### 首页添加  topic 和metrics 链接

![1](https://github.com/zhoulaosan/vernemq_plugs/blob/master/readme-img/1.png)

#### 此处填写你设置的账号密码

![2](https://github.com/zhoulaosan/vernemq_plugs/blob/master/readme-img/2.png)

Topic
![3](https://github.com/zhoulaosan/vernemq_plugs/blob/master/readme-img/3.png)
平台信息监控
![4](https://github.com/zhoulaosan/vernemq_plugs/blob/master/readme-img/4.png)
![5](https://github.com/zhoulaosan/vernemq_plugs/blob/master/readme-img/5.png)

页面模拟CMD 可做一些设置
![6](https://github.com/zhoulaosan/vernemq_plugs/blob/master/readme-img/6.png)



## 安裝

### centos环境

```
官网下载pem 文件
$ yum install -y
$ whereis vernemq
$ cd /usr/lib64/vernemq
$ vernemq version
```

## VMQ HTTP API 使用

#### 1.配置  

​	vim /ect/vernemq/vernemq.conf

​	参考 https://docs.vernemq.com/monitoring/introduction

​	或参考  项目中 vernemq.conf  和 vmq.acl

#### 2.创建http API 密钥

```shell
cd /usr/lib64/vernemq/bin
#自动生成的密钥,账号密码都可以填他
./vmq-admin api-key create
	2sDc5Y2y1AHHU8hpuuIgbVhCvbBFVuei 
# 或者手动创建
./vmq-admin add key=mykey
./vmq-admin api-key show
```

​	测试链接

```
http:127.0.0.1:8888/api/v1/session/show
http://127.0.0.1:8888/api/v1/listener/show
http://127.0.0.1:8888/api/v1/plugin/show
```
#### 3.HTTP命令

显示客户端链接
vmq-admin session show --topic --client_id

HTTPAPI test
http://127.0.0.1:8888/api/v1/session/show?&--node&--mountpoint&--client_id&--queue_pid&--queue_size&--session_pid&--is_offline&--is_online&--statename&--deliver_mode&--offline_messages&--online_messages&--num_sessions&--clean_session&--is_plugin&--queue_started_at&--user&--peer_host&--peer_port&--protocol&--waiting_acks&--session_started_at&--topic&--qos&--rap&--no_local

#### 4.展示

​	修改源码js
​			前端代码位置
​				/usr/lib64/vernemq/lib/vmq_server-1.10.2/priv/static

#### 5.metrics

​		linux命令
​			vmq-admin metrics show
​			vmq-admin metrics show --with-descriptions
​		http转换
​			http://127.0.0.1:8888/api/v1/metrics /show?&--with-descriptions


#### 6.拓展
拓展
	erlang语言
			解决并发问题
	Prometheus
			Prometheus是由SoundCloud开发的开源监控报警系统和时序列数据库(TSDB)。Prometheus使用Go语言开发，是Google BorgMon监控系统的开源版本。

#### 7.官方API
https://docs.vernemq.com/administration/http-administration

```

```