# JDK_8.0

发布时间：2014-3-18

代号：Spider（蜘蛛）

重大改变：Lambda表达式、内置Nashorn JavaScript、彻底移除HotSpot的永久代



## 版本新特征

### 1，引入Lambda 表达式



###  2，管道和流



### 3，引入了新的Date-Time API(JSR 310)来改进时间、日期的处理

```java
  	// 获取当前日期
    LocalDate now = LocalDate.now();
    // 设置日期
    LocalDate now2 = LocalDate.of(2099, 2, 28);
    // 解析日期，格式必须是yyyy-MM-dd
    LocalDate now3 = LocalDate.parse("2018-01-12");
    DateTimeFormatter dtf = DateTimeFormatter.ofPattern("yyyy/MM/dd");
    String formatRs = now.format(dtf);
    // 取本月第一天
    LocalDate firstDay = now.with(TemporalAdjusters.firstDayOfMonth());
    LocalDate firstDay2 = now.withDayOfMonth(1);
    // 取本月第2天
    LocalDate secondDay = now.withDayOfMonth(2);
    LocalDate nextMonthDay = now.with(TemporalAdjusters.firstDayOfNextMonth());
    LocalDate nextYearDay = now.with(TemporalAdjusters.firstDayOfNextYear());
    // 明年的这一天
    LocalDate localDate = now.plusYears(1);
    // 当前日期加上往后推20天
    LocalDate plusDate = now.plus(20, ChronoUnit.DAYS);
    LocalDate plusYear = now.plus(10, ChronoUnit.YEARS);
    // 当前日期往前推10天
    LocalDate minusDay = now.minusDays(10);
    LocalDate minusYear = now.minus(10, ChronoUnit.YEARS);
    //localDate转Date
    ZoneId zoneId = ZoneId.systemDefault();
    ZonedDateTime zdt = now.atStartOfDay(zoneId);
    Instant instant = zdt.toInstant();
    Date fromDate = Date.from(instant);
    // Date转LocalDate
    Date date = new Date();
    Instant instantToUse = date.toInstant();
    ZoneId zoneIdToUse = ZoneId.systemDefault();
    LocalDate localDateToShow = instantToUse.atZone(zoneIdToUse).toLocalDate();
    // 比较日期大小
    boolean b1 = localDateToShow.equals(LocalDate.of(2018, 04, 27));
    boolean b2= localDateToShow.equals(LocalDate.of(2018, 04, 26));
    // 判断日期前后  -> false
    boolean b3 = localDateToShow.isAfter(LocalDate.of(2018, 04, 26));//false
    boolean b4 = localDateToShow.isAfter(LocalDate.of(2018, 04, 25));//true
    boolean b5 = localDateToShow.isBefore(LocalDate.of(2018, 04, 26));//false
    boolean b6 = localDateToShow.isBefore(LocalDate.of(2018, 04, 25));//false
    boolean b7 = localDateToShow.isBefore(LocalDate.of(2018, 04, 27));//true
    // 计算两个日期之间的时间间隔   格式为：x年x月x天
    Period between = Period.between(localDateToShow, LocalDate.of(2018, 05, 28));
    long bwDays = ChronoUnit.DAYS.between(localDateToShow, LocalDate.of(2018, 05, 28));
```

### 4，默认的方法（接口可以编写默认的方法）



### 5，Nashorn javascript引擎（允许java运行特定JavaScript代码）



### 6，Optional class (处理nullPointException)



### 7，并行累加器



### 8，并行操作



### 9，内存错误移除



### 10，TLS SNI 服务器名称标识(Server Name Identification)



### 11，函数式编程



### 12，重复注解















