# stat

**stat** 命令查看一个或多个文件或目录状态，而且额外输出一列文件或目录修改时间与当前时间的间隔，时间单位为秒.

### 1 用法

    stat [path]...

### 2 选项
	文件路径说明
	文件路径除了支持linux/windows传统表示法，同时还支持&#39;/&#39;跨平台表示法。示例如下:
	传统:
	linux:&#39;/tmp/test.txt&#39; 或 "/tmp/test.txt"
	windows:&#39;c:\tmp\test.txt&#39; 或 "c:\\tmp\ltest.txt"  ##双引号内&#39;\&#39;需要转义
	
	跨平台:
	linux:&#39;/tmp/test.txt&#39; 或 "/tmp/test.txt"
	windows:&#39;c:/tmp/test.txt&#39; 或 "c:/tmp/test.txt'
	路径中没有空格可以省略&#39;&#39;&#39; 或 &#39;"&#39;,例如:cat/tmp/test.txt 或 cat c:/tmp/test.txt


### 3 示例

##### 查看/tmp/test.txt,/tmp/test1.txt状态，命令如下：
    stat /tmp/test.txt /tmp/test1.txt
	
##### 输出:
	[
	  {
		"IsDir":false,
		"ModDelay":38.095691861,
		"ModTime":"2020-03-07T11:45:37+08:00",
		"Mode":420,
		"Name:"test.txt",
		"Size":10,
		"message":"found",
		"status":true,
		"path":"/tmp/test.txt"
	  },
	  {
		"ModDelay":1583552775,
		'message":"lstat /tmp/test1.txt: no such file or directory",
		"status":false,
		"path" :"/tmp/test1.txt"
	  }
	]
	