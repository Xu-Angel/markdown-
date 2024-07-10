# datetime

**datetime** datetime命令按指定格式输出时间字符串。

### 1 用法

    datetime (options}

### 2 选项

    -f 时间格式化标记字符串
	-d 时间间隔。
	-u 时间间隔单位,默认为分钟。

#### 2.1 时间格式化标记



#### 2.2 时间间隔单位
- y, year, years
- Q,quarter, quarters
- M,month,months
- w, week,weeks
- d,day, days
- h,hour,hours
- m,minute,minutes
- s,second,seconds
- ms,milisecond,milliseconds
- ns,nanosecond,nanoseconds


### 3 示例

#### 3.1当前时间按YYYY-MM-DDH:m:ss格式化,命令如下:
    datetime -f'YYYY-MN-DD HH:mm:ss
##### 输出:
    2020-03-0611:28:04
####  3.2当前时间减去5分钟后按YYYY-MW-DDHH:mm:ss格式化,命令如下:
    datetime -f'YYYY-MM-DD HH:mm:ss'-d-5 -u m
##### 输出:
    2020-03-8611:23:04
