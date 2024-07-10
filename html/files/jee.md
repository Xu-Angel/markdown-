# jee

JSON表达式评估器，通过逻辑和数学表达式转换JSON。jee设计用于流处理并实现JSON数据简单的数学计算。

### 1 使用说明
#### 1.1 JSON查询
获取整个输入对象:
    
    > echo '{"a":3}'| jee
	{
		a':3
	}
	
获取特定键的值:

	> echo '{"a":3,"b": 4}|jee '.a'
    3
从数组获取值

	echo '{"a":[4,5,6]}'| jee '.a[0]'
	4

从数组获取所有值:

	> echo '{"a":[4,5,6]}'| jee '.a[]'
	[
      4,
	  5,
      6
	]

查询数组'a'内的所有对象以获取键'id':

	> echo '{"a": [{"id":"foo"},{"id":"bar"},{"id":"baz"}]}'|jee '.a[].id'
	[
	  "foo",
	  "bar",
	  "baz'
	]

#### 1.2 JSON运算
##### 1.2.1 基本运算

`+ - * /`

	> echo '{"a":10}' | jee '(.a * 100)/-10 * 5'
	-500
##### 1.2.2 比较运算

`\> >= < <= !=`

	> echo '{"a":10}' | jee '(.a * 100)/-10 * 5 == -500'
	true
	> echo '{"a":10}' | jee'(.a*100)/-10 * 5 > 0'
	false

##### 1.2.3 逻辑运算

`1| &&`

	> echo '{"a": false}'| jee '!(.a && true) || false == true
	true

#### 1.3 内置函数
##### 1.3.1 类型转换
	$num(x{bool,float64,string, nil})

将x转换为foat64。如果x是布尔值，则返回1表示true，0表示false。如果x为零，则返回0.

	$str(x{bool,float64,string,nil,object,[]*))
将x转换为字符串。如果x是布尔值，则将“ true”返回true，将“ false”返回false。返回“ nul”"为零。如果x是对象或数组，则将
其封送为JSON字符串。

	$bool(x{bool, string})
将x转换为布尔值。

	$~bool(x{bool,float64,string, nil, object, []*})
将x真正转换为布尔值。假值:nul，NaN，0，false和长度为0的数组
##### 1.3.2 算数相关
	$sqrt(x float64)
返回x的平方根。

	$pow(x float64,y float64)
	
返回x^y。

	$floor(x float64)
返回x的最接近的向下整数:

	$abs(x float64)
返回x的绝对值。
##### 1.3.3 数组(array)

	$len(a []interface{})
返回数组a的长度，

	$has( a {[]bool,[]float64,[]string,[]nil},val {bool, float64,string, nil})
检查数组是否包含val。返回布尔值。val不能是对象。

	$sum(a []float64)
返回数组的总和，

	$min(a []float64)
返回数组的最小值。

	$max(a []float64)
返回数组的最大值。

	$avg(a []float64)
返回数组的平均值，精确到小数点后三位，

	$first(a []float64)
返回数组的第一个元素。

	$last(a []float64)
	
返回数组的最后一个元素。
##### 1.3.4 对象(object)

	$keys(o object)

返回对象o中的键数组，

	$exists(o object, key string)
检查对象中是否存在键值。
##### 1.3.5 日期和时间
	$now()
返回当前系统时间，以foat64(毫秒)为单位，

	$parseTime(layout string,t string)
接受golang时间格式的时间布局。t被解析并以float64(毫秒)数返回

	$fmtTime(layout string,t float64)
接受golang时间格式的时间布局。t以foat64(毫秒)为单位。返回格式化的字符串
##### 1.3.6 字符串
	$contains(s string,substr string)
字符串中是否包含子字符串。

	$regex(pattern string,s string)
正则匹配字符串。

### 2 相关限制
- 数据运算为强类型匹配，falsell"foo"将会生产类型匹配错误,
- null和0不为假。
- 当前不评估使用JSON键作为数组索引或括号表示中的转义键。即:.aГ.b下
- jee查询中的所有数字都必须以数字开头。数字应该以0开头。 使用 0.1 代替.1
- 方括号表示法可用于需要转义的键。.["foo"]["bar"]]
- 对不存在的JSON键或索引的查询返回null(要测试键是否存在，请使用$exists)
- jee不支持变量，条件表达式或赋值。