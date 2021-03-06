# FISCO-BCOS浏览器监控上报脚本

## 一、功能介绍

监控上报脚本，能够自动读取区块链节点的统计日志，并将相应的统计参数上报给server端。

## 二、使用方式

### 1、准备

每台部署了区块链节点的机器仅运行一个脚本即可。

> 使用前，请将需要被监控的区块链节点配置文件中的statlog打开。

```shell
vim config.json
```

> 配置后的config文件中statlog参数如下：

```json
"statlog": "ON",
```

### 2、配置参数

> 进入区块链浏览器根目录下的report文件夹，修改ReportAgent.py

```shell
cd report
vim ReportAgent.py
```

> 配置步骤
>
> （1）配置上报周期：ACCESS_NODE_INTERVAL，默认60秒即可
>
> （2）配置server端IP：BROWSER_SERVER_IP
>
> （3）配置server端接收上报数据的端口：BROWSER_SERVER_PORT
>
> （4）配置节点信息对象。若有多个节点，则依次按照举例定义。
>
> （5）将定义的节点信息对象写入全局数组（```nodes```）中。

```python
ACCESS_NODE_INTERVAL = 60 #60s 多久询问、上报一次node的信息

HOST_IP = "123.207.123.123" #本机器的外网IP，仅作为浏览器端区分是哪台机器上报的数据
BROWSER_SERVER_IP = "10.107.105.138" #上报server端的IP
BROWSER_SERVER_PORT = "8088" #上报server端的端口

node0 = ["node0", "/bcos-data/node0/log/", 8545] #node的名字，node的log目录, RPC端口号
node1 = ["node1", "/bcos-data/node1/log/", 8546] #node的名字，node的log目录, RPC端口号

nodes = [node0, node1]
```

### 3、启动脚本

```shell
./start_Agent.sh
```

### 4、查看日志

```shell
tail -f agentOut.txt
```

### 5、关闭脚本

```shell
./stop_Agent.sh
```





