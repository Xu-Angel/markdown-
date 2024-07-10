# ping

**ping** 命令用于查看操作系统进程相关信息

### 1 用法

    ping {options} [host] ...

### 2 选项
	-c ping包的个数，默认值为3。
	-t 连接超时，单位为秒。默认值为5秒。
	-j 提供多台主机+端口的执行并发度，默认值为10。
多个主机之间可以用空格或 ',' 分隔。

### 3 示例
测试10.211.55.8和10.211.55.16主机的连通状态，命令如下：
	
	ping 10.211.55.8 10.211.55.16
输出

	[
	  {
		"AvgRtt":0,
		"Host":"18.211.55.8",
		"LossPercent":0,
		"MaxRtt":0,
		"MinRtt":0,
		"PkgLoss" :0,
		"PkgRecv" : 3,
		"PkgSent":3,
		"StdDevRtt":0,
		"_message":"ping finished",
		"_status":true
	  },
	  {
		"AvgRtt":0,
		"Host":"10.211.55.16",
		"LossPercent":100,
		"MaxRtt":0,
		"MinRtt":0,
		"PkgLoss":3,
		"PkgRecv":0,
		"PkgSent":3,
		"StdDevRtt":0,
		"_message":"ping finished",
		"_status":true
	  }
	]