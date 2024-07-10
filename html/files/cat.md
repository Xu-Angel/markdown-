# cat

**cat** 命令显示一个或多个文件内容

### 1 用法

    cat [file path]...

### 2 选项

    文件路径说明
	文件路径除了支持Linux/windows传统表示法,同时还支持'/跨平台表示法。示例如下:
	传统:
	linux: '/tmp/test.txt'或"/tmp/test.txt"
	windows:'c:\tmp\test,txt'或"c:\\tp\\test.txt"##双引号内\'需要转义
	
	跨平台
	Linux:'/tmp/test.txt'或"/tmp/test.txt"

	windows:'c:/tmp/test.txt'或"c:/tmp/test.txt"
	路径中没有空格可以省略'''或'"",例如:cat/tmp/test.txt或catc:/tmp/test.txt


### 3 示例

##### 显示多个文件，命令如下：
    cat /tmp/test1.txt /tmp/test2.txt
	
##### 输出:
    line in test1
	Line in test2
	
