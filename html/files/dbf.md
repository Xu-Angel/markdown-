# dbf

**dbf** 命令从dbf文件中读取数据并转换成ison对象数组:

### 1 用法

    dbf {options} [dbf file]

### 2 选项
	-o 开始读取偏移数。默认从0开始。
	-l 读取对象数限制。默认为8，不限制。
	-c 显示的字段名称，以'，'分隔。默认为空，显示所有字段。
	-C 字符集，默认为win1250。支持:win1250 和utf8。
	-j 结果过滤jee表达式。
	-f 行过滤jee表达式。
	-S 输出总行数。

### 3 示例
示例文件/tmp/test.dbf内容




#### 3.1 默认解析并只显示ID,BOOL,FLOAT列。命令如下
	dbf -c 'ID,BOOL,FLOAT' /tmp/test.dbf
输出

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
	
#### 3.2 只读取第一行并计算DATUM列时间与当前时间相差的天数。命令如下:

输出

#### 3.3 只读取第2行并且拼接TD列和COMP_OS列。命令如下
	dbf -o 1 -l 1 -j '$str(.[0].ID)+ " - " + .[0].COMP_OS' /tmp/test.dbf
输出

#### 3.4 读取B00L列为true所有行并且只显示ID,BOOL,FLOAT
	dbf -c "ID,BOOL,FLOAT" -f ".B00L == true" /tmp/test.dbf
输出
#### 3.5 计算ID列的平均值。命令如下
	dbf -j '$avg(.[].ID)' /tmp/test.db
输出