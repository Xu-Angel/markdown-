# logfile
**logfile** 命令实现对日志文件的增量读取。

### 1 用法
	logfile (options} [logfile]

### 2 选项
	-c 日志文件字符集，默认为utf8
	-x 按行排除正则表达式
	-n 按行包含正则表达式，-x按行排除优先
	-k 第一次读取跳过已存在的行
	-d 清除当前文件的状态记录，下次将从头读取文件
	-C 仅输出行数


支持如下字符集选项:

	"US-ASCII", "ASCII", "US", "ISO646-US", "IBM367","Cp367", "ANSI X3.4-1968", "iso-ir-6", "ANSI X3.4-1986", "IS0 646"
	"IS0-8859-1", "latin1", "Iso Latin 1", "IBM819", "cp819", "IS0 8859-1:1987", "iso-ir-188","l1", "csISolatin1"
	"Big5","csBig5"
	"EUC-JP", "extended unix code packed format for japanese","cseucpkdfmtjapanese'
	"GB18030"
	"GBK"
	"Shift JIs","Ms Kanji","csShiftJIs", "SJIS"
	"UTF-16","UTF-16BE","UTF-16LE"
	"UTF-8"

### 3 示例
示例文件/tmp/test.log内容

	info user line 1
	warn user line 2
	warn sys  line 3
	warn sys  line 4
	warn user line 5

#### 3.1 增量读取日志文件示例。

##### 3.1.1 第一步，第一次读取日志文件
	/tmp/test.log
输出

	info user line 1
	warn user line 2
	warn sys  line 3
	warn sys  line 4
	warn user line 5
	
##### 3.1.2 第二步，向日志文件新写入一行
	echo 'warn user line 6'>> /tmp/test.log

##### 3.1.3 第三步，再次读取日志文件
	logfile /tmp/test.log
输出

	warn user line 6
#### 3.2第一次执行跳过已存在行，并且只读取包含error或warn关键字且不包含sys关键字的行。
##### 3.2.1 开始读取:
	logfile /tmp/test.log -k-x'sys'-n 'errorlwarn
因命令加-k参数跳过存在行，输出为空
##### 3.2.2 向日志文件写入新记录
	echo 'warn user line 6'>> /tmp/test.log
	echo 'warn sys line 7'>> /tmp/test.log
	echo 'error user line 8'>> /tmp/test.log

##### 3.2.3 继续读取，命令如下:
	logfile /tmp/test.log-k-x&#39;sys&#39;-n &#39;errorlwarn&#39;

因logfile已经执行过一次，-k参数被忽略，日志为增量读取，line 7不满足过滤条件被忽略，输出如下:
	
	warn user line 6
	error userline 8
#### 3.3 清除logfile状态示例
##### 3.3.1 读取日志文件，命令如下:
	logfile /tmp/test.log
输出

	info user line 1
	warn user line 2
	warn sys  line 3
	warn sys  line 4
	warn user line 5
##### 3.3.2 向日志文件写入新记录
	echo &#39;warn user line 6&#39;>> /tmp/test.log
##### 3.3.3 继续读取日志文件logfile /tmp/test.log
输出

	warn user line 6
##### 3.3.4 清除日志文件状态
	logfile /tmp/test.log -d

##### 3.3.5 继续读取日志文件
	logfile /tmp/test.log
因为已经清除状态，将从头读取日志文件，输出如下:

	info user line 1
	warn user line 2
	warn sys  line 3
	warn sys  line 4
	warn user line 5
	warn user line 6