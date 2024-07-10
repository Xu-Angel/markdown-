# process

**process** 命令用于查看操作系统进程相关信息

### 1 用法

    stat [path]...

### 2 选项
	-m 进程内存使用状态。
	-d 进程磁盘I0使用状态。
	-w 进程网络I0使用状态，仅支持linux。
	-t 进程的线程状态，仅支持linux。
	-T 进程cpu使用状态。
	-a 配合-w选项，显示所有网络接口，默认为总体网络，仅支持linux。
	-c 进程数量。
	-C 线程数量。
	-i 计算性能数据时间间隔，默认值为1秒。

### 3 示例
#### 3.1 查看系统所有进程，命令如下:
	process
#### 3.2 查看名称为dlhost.exe(windows)或demo-agent(linux)的所有进程状态，命令如下
	process dllhost.exe #windows
	#或
	process demo-agent #linux

windows输出

	[
	  {
		"Background" :false
		"CPUPercent" :0,
		"Cmdline":"c:\Windows\system32\dllhost.exe /Processid:(02D4B3F1-FD88-11D1-960D-00805FC79235}"
		"CreateTime":1583251021631,
		"Cwd" :"".
		"Exe":"C:\Windows\System32\dllhost.exe",
		"Foreground" :false,
		"IOnice":0，
		"IsRunning" :true ,
		"MemoryPercent":0.27
		"Name" :"dllhost.exe"
		"Nice":8,
		"NumFDs" : 0 ,
		"NumThreads" : 13,
		"Ppid":520，
		"Status" :"".
		"Tgid" :0,
		"Username" :"NT AUTHORITY\SYSTEM"
		"_message" :"found",
		"_status":true
	  },
	  {
		"Background" :false,
		"CPUPercent" :0,
		"Cmdline":"c:\windows\system32\dllhost.exe /Processid:{A2299D9D-1E8D-4CE6-AC99-34F3A5939AFB}"
		"CreateTime":1583251021210,
		"Cwd" :""
		"Exe":"C:\Windows\System32\dllhost.exe",
		"Foreground" :false,
		"IOnice":0.
		"IsRunning" :true ,
		"MemoryPercent" :0.16,
		"Name":"dllhost.exe"
		"Nice" :8,
		"NumFDs" :0,
		"NumThreads" :7,
		"Ppid":520,
		"Status":""
		"Tgid" :0,
		"Username":"NT AUTHORITY\SYSTEM"
		"_message" :"found",
		"_status":true
	  }
	]
linux输出

	[
	  {
		"Background" :true ,
		"CPUPercent":0.01.
		"Cmdline":"/opt/demo-agent/demo-agent"
		"CreateTime":1583541097000,
		"Cwd" :"/opt/demo-agent",
		"Exe":"/opt/demo-agent/demo-agent"
		"Foreqround" :false.
		"IOnice":0.
		"IsRunning" :true ,
		"MemoryPercent" :0.99
		"Name" :"demo-agent",
		"Nice":20.
		"NumFDs" :11,
		"NumThreads" :10,
		"Ppid":1,
		"Status":"S",
		"Tgid" :11115,
		"Username" :"root",
		"_message" :"found",
		"_status":true
	  }
	]

#### 3.3 查看demo-agent进程网络I0使用状态，命令如下:
	process -w demo-agent  #windows 下进程名要加.exe扩展，例如:demo-agent.exe
	
输出

	[
	  {
		"BytesRecv" :0,
		"BytesSent":249.
		"Dropin" :0,
		"Dropout" :0,
		"Errin" :0,
		"Errout":0
		"Fifoin":0.
		"Fifoout":0,
		"Name" :"demo-agent",
		"PacketsRecv" :0,
		"PacketsSent":1.
		"_message":"found"
		"_status":true
	  }
	]
#### 3.4 查看demo-agent进程内存使用状态，命令如下:
	process -m demo-agent  #windows下进程名要加.exe扩展，例如:demo-agent.exe

输出

	[
	  {
		"Data" :0,
		"HWM" : 0 ,
		"Locked" :0.
		"Name" :"demo-agent",
		"RSS":23040000,
		"Stack" :0,
		"Swap" :0 ,
		"VMS":496975872,
		"_message" :"found",
		"_status" :true
	  }
	]
#### 3.5 查看demo-agent进程磁盘IO使用状态,命令如下:
	process -c demo-agent  #windows下进程名要加.exe扩展，例如:demo-agent.exe

输出

	[
	  {
		"Name":"demo-agent",
		"ReadBytes" :0,
		"ReadCount" :2,
		"WriteBytes" :0,
		"WriteCount":0,
		"_message" :"found",
		"_status":true
	  }
	]
#### 3.6 查看名称为demo-agent进程的数量，命令如下:

	process -c demo-agent  #windows下进程名要加.exe扩展，例如:demo-agent.exe

输出

	[
	  {
		"Count":10
	  }
	]
#### 3.7 查看名称为demo-agent1进程不存在状态，命令如下:
	process -C demo-agent1  #windows 下进程名要加.exe扩展，例如:demo-agent1.exe
	
输出

	[
	  {
		"Name" :"demo-agent1"
		"_message":"not found"
		"_status":false
	  }
	]