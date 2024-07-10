# telnet

**telnet** telnet命令用来测试目标主机tcp端口状态。

### 1 用法

    telnet [host port] ...

### 2 选项
	-t 连接超时,单位为秒。默认值为5秒。
	-j 提供多台主机+端口的执行并发度，默认值为2


### 3 示例
测试10.211.55.8和10.211.55.16主机的22号端口状态,命令如下
teLnet 10.211,55,8 22 10.211.55.16 22

输出

	[
	  {
		"CostNS":686468,
		"Host":"10.211.55.8",
		"Port":"22",
		"_message":"connected",
		"_status":true
	  },
	  {
		"CostNS":3001385457,
		"Host":"10.211.55.16",
		"Port":"22",
		"_message":"dial tcp 10.211.55.16:22:connect:no route to host",
		"_status":false
	  }
	]