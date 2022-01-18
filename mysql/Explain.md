# MYSQL Explain

​	使用EXPLAIN关键字可以模拟优化器执行SQL语句，分析查询语句或是结构的性能瓶颈，查看该SQL语句有没有使用上了索引，有没有做全表扫描。在select语句之前增加explain关键字，MySQL会在查询上设置一个标记，执行查询会返回执行计划的信息，而不是执行SQL。

​	expain出来的信息有10列，分别是**id、select_type、table、type、possible_keys、key、key_len、ref、rows、Extra**。

## id

​	SQL执行的成功的标识，SQL从大到小的执行。id相同时，执行顺序由上至下，内存会认为三个表，乘积小的先执行。如果是子查询，id的序号会递增，id值越大优先级越高，越先被执行；id如果相同，可以认为是一组，从上往下顺序执行；在所有组中，id值越大，优先级越高，越先执行。

## select_type

​	表示对应行是简单还是复杂的查询。

| 类型            | 描述                                                |
| --------------- | --------------------------------------------------- |
| SIMPLE          | 最简单的select(不使用UNION或子查询等)               |
| PRIMARY         | 最外层的select，主查询                              |
| UNION           | UNION中的第二个或后面的select语句                   |
| DEPENDENT UNION | UNION中的第二个或后面的select语句，取决于外面的查询 |
| SUBQUERY        | 子查询中的第一个select，取决于外面的查询            |
| DERIVED         | 派生表的select                                      |

## table

​	代表表名。有时不是真实的表名,看到的是<derived**X**>(数字X是第几步执行的结果)。

## type

​	表示关联类型或访问类型，即MySQL决定如何查找表中的行，查找数据行对应的大概范围。

​	依次从最优到最差的分别为：system>const>eq_ref>ref>range>index>All。一般来说，得保证查询达到range级别，最好达到ref。

​	NULL：MySQL能够在优化阶段分解查询语句，在执行阶段用不着在访问表或索引。例如：在索引列中选取最小值，可以单独查找索引来完成，不需在执行时访问表。

| 类型          | 描述                                                         |
| ------------- | ------------------------------------------------------------ |
| ALL           | 进行全表扫描                                                 |
| index         | 全索引扫描。index与ALL区别为index类型只遍历索引树            |
| range         | 只检索给定范围的行，使用一个索引来选择行                     |
| ref           | 表示上述表的连接匹配条件，即哪些列或常量被用于查找索引列上的值 |
| eq_ref        | 类似ref，区别就在使用的索引是唯一索引，对于每个索引键值，表中只有一条记录匹配，简单来说，就是多表连接中使用primary key或者 unique key作为关联条件 |
| const、system | 当MySQL对查询某部分进行优化，并转换为一个常量时，使用这些类型访问。如将主键置于where列表中，MySQL就能将该查询转换为一个常量,system是const类型的特例，当查询的表只有一行的情况下，使用system |

## possible_keys

​	select可能会使用哪些查询来查找。explain时可能会出现possible_keys有列，而key显示为NULL的情况，这种情况是因为表中的数据不多，会认为索引对此查询帮助不大，选择了全表扫描。如果该列为NULL，则没有相关的索引。这种情况下，可以通过检查where子句看是否可以创造一个适当的索引来提高查询性能，然后用explain查看效果

## Key

​	显示实际采用哪个索引对该表的访问。如果没有使用索引，则改列为NULL。如果想强制使用或忽视possible_keys列中的索引，在查询中使用force index、 ignore index。

## key_len

​	这一列显示了在索引里使用的字节数，通过这个值可以估算出具体使用了索引中的哪些列。

​	如果字段允许为NULL，需要1字节记录是否为NULL。索引最大长度是768字节，当字符串过长时，会做一个类似做前缀索引的处理，将前半部分的字符串提取出来做索引。

## ref

​	显示了在key列记录的索引中，表查找值所用到的列或常量，常见的有： const(常量)，字段名等。一般是查询条件或关联条件中等号右边的值，如果是常量那么ref列是const，非常量的话ref列就是字段名。

## row

​	估计要读取并检测的行数，注意这个不是结果集的行数。

## Extra

​	额外信息。

| 类型                  | 描述                                                         |
| --------------------- | ------------------------------------------------------------ |
| Using index           | 使用覆盖索引（结果集的字段是索引，即select后的film_id        |
| Using index condition | 查询的列不完全被索引覆盖，where条件中是一个前导的范围        |
| Using where           | 使用where语句来处理结果，查询的列未被索引覆盖                |
| Using temporary       | 需要创建一张临时表来处理查询。出现这种情况一般要进行优化，首先要想到是索引优化 |
| Using filesort        | 将用外部排序而不是索引排序，数据较小时从内存排序，否则需要在磁盘完成排序。这种情况下一般也是要考虑使用索引来优化的 |



参考文献：https://www.cnblogs.com/xiaoqiang-code/p/11404149.html