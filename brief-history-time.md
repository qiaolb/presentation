# 时间简史
Joe

[https://qiaolb.github.io](https://qiaolb.github.io)



# 概念
<!-- section data-transition="zoom" -->



## 时间定义
<!-- section data-transition="fade" -->
* 时间是物理学中的基本物理量之一
* 宇宙大爆炸“之前”没有时间可言 <!-- .element: class="fragment" -->
* “永远向前”指时间的增量总是正数 <!-- .element: class="fragment" -->
* 时间表达物件的生灭排列 <!-- .element: class="fragment" -->



## 时间单位
<!-- section data-transition="fade" -->
* 基本单位是秒
* 1s = 铯-133的原子基态的两个超精细能阶间跃迁对应辐射的9,192,631,770个周期的持续时间 <!-- .element: class="fragment" -->
* 毫秒ms、分min、小时h、日（天）d、月m、年y等 <!-- .element: class="fragment" -->



## 历法
* 推算年、月、日，并使其与相关天象对应的方法，是协调历年、历月、历日和回归年、朔望月和太阳日的办法 <!-- .element: class="fragment" -->
* 根据天象变化的自然规律，计量较长的时间间隔   <!-- .element: class="fragment" -->
* 公历，农历……  <!-- .element: class="fragment" -->



## 闰年
* Leap Year  <!-- .element: class="fragment" --> 
* 弥补因人为历法规定造成的年度天数与地球实际公转周期的时间差而设立的  <!-- .element: class="fragment" -->
* 闰秒    <!-- .element: class="fragment" -->



## 时区
<!-- section data-transition="fade" -->
* 地球表面按经线划分的24个区域 <!-- .element: class="fragment" -->
* 按经线从东到西  <!-- .element: class="fragment" -->
* 相邻区域的时间相差1小时 <!-- .element: class="fragment" -->
* 为了照顾到行政上的方便，常将1个国家或 1个省份划在一起 <!-- .element: class="fragment" -->
* 北京时间：东八区。 中国，跨5个时区，东八区  <!-- .element: class="fragment" -->
* 世界时（UT）和 协调世界时（UTC）  <!-- .element: class="fragment" -->



## 时区的意义
<!-- section data-transition="slide-in fade-out" -->
* 早上9点，上班时间
* 中午12点钟，该去南窑国际吃饭了
* 晚上6点后，遛狗、逛街……




## 夏令时
<!-- section data-transition="slide-in fade-out" -->
* Daylight Saving Time：DST <!-- .element: class="fragment" -->
* 一种制度   <!-- .element: class="fragment" -->
* 在天亮早的夏季人为将时间调快一小时   <!-- .element: class="fragment" -->
* 目的：早睡早起，减少照明量，以充分利用光照资源，从而节约照明用电   <!-- .element: class="fragment" -->



## 夏令时现状
* 中国：已经废弃
* 俄罗斯：永久使用
* 美国：由各州、各县自行决定
* 加拿大，欧盟……



# 计算机中的时间
<!-- section data-transition="zoom" -->



## 从哪儿获得时间
* CMOS保存
* NTP： Network Time Protocol



## 计算机的时间
* 从1970年开始   <!-- .element: class="fragment" -->
* 千年虫问题   <!-- .element: class="fragment" -->
* 32位、64位   <!-- .element: class="fragment" -->



# 程序时间



## 基本概念
* 起点： 1970年1月1日 00:00:00   <!-- .element: class="fragment" -->
* 时间戳：整数，从起点计算，单位： ms/s   <!-- .element: class="fragment" -->
* format： 字符串   <!-- .element: class="fragment" -->



#Java的时间



## Java 8之前的时间
* java.util.Date
* java.text.DateFormat
* java.text.SimpleDateFormat
* java.util.Calendar



## Java 8之前时间问题
* 可变性。像时间和日期这样的类应该是不可变的   <!-- .element: class="fragment" -->
* 偏移性。Date中的年份是从1900开始的，而月份都是从0开始的   <!-- .element: class="fragment" -->
* 命名。Date不是“日期”，而Calendar也不真实“日历”   <!-- .element: class="fragment" -->
* 格式化。格式化只对Date有用，Calendar则不行。另外，它也不是线程安全的   <!-- .element: class="fragment" -->



## Java 8的时间
* java.time – 包含值对象的基础包
* java.time.chrono – 提供对不同的日历系统的访问
* java.time.format – 格式化和解析时间和日期
* java.time.temporal – 包括底层框架和扩展特性
* java.time.zone – 包含时区支持的类



## LocalDate
* 不可变类型  <!-- .element: class="fragment" -->
* 不包含时间  <!-- .element: class="fragment" -->
* 不包含时区  <!-- .element: class="fragment" -->



## LocalDate用法
```java
LocalDate date = LocalDate.of(2017, Month.May, 10);
int year = date.getYear(); // 2017
Month month = date.getMonth(); // 5月
int dom = date.getDayOfMonth(); // 10
DayOfWeek dow = date.getDayOfWeek(); // 星期三
int len = date.lengthOfMonth(); // 31 （5月份的天数）
boolean leap = date.isLeapYear(); // false （不是闰年）
```
<!-- .element: class="fragment" -->

```Java
LocalDate date = LocalDate.of(2014, Month.JUNE, 10);
date = date.withYear(2015); // 2015-06-10
date = date.plusMonths(2); // 2015-08-10
date = date.minusDays(1); // 2015-08-09
```
<!-- .element: class="fragment" -->

```java
import static java.time.DayOfWeek.*
import static java.time.temporal.TemporalAdjusters.*
  
LocalDate date = LocalDate.of(2014, Month.JUNE, 10);
date = date.with(lastDayOfMonth());
date = date.with(nextOrSame(WEDNESDAY));
```
<!-- .element: class="fragment" -->



## 不同的历法系统
* LocalDate是固定于单个历法系统的：公历（由ISO-8601标准定义）   <!-- .element: class="fragment" -->
* 不必跟GregorianCalendar一致。凯撒历和格里高利历之间有一个转换日    <!-- .element: class="fragment" -->
* Chronology接口，处理其他历法系统    <!-- .element: class="fragment" -->
* Java 8支持额外的4个历法系统：泰国佛教历（ThaiBuddhistDate），中华民国历（MinguoDate），日本历（沿袭中国古代帝位纪年）（JapaneseDate），伊斯兰历（HijrahDate）    <!-- .element: class="fragment" -->



## 时间处理
* LocalTime
* LocalDateTime



## 时间点
* java.time.Instant       <!-- .element: class="fragment" -->
* 表示时间线上的一点    <!-- .element: class="fragment" -->
* 不需要任何上下文信息，例如，时区       <!-- .element: class="fragment" -->
* 自1970年1月1日0时0分0秒（UTC）开始的秒数       <!-- .element: class="fragment" -->
* java.time包是基于纳秒       <!-- .element: class="fragment" -->



## 时间点示例
```java
Instant start = Instant.now();
// perform some calculation
Instant end = Instant.now();
assert end.isAfter(start);
```



## 时区
* TimeZone ---> ZoneId      <!-- .element: class="fragment" -->
* ZoneId是不可变的     <!-- .element: class="fragment" -->
* ZoneDateTime负责处理面向人类解释时间和时区     <!-- .element: class="fragment" -->




## 时区用法
```java
ZoneId zone = ZoneId.of("Europe/Paris");
  
LocalDate date = LocalDate.of(2014, Month.JUNE, 10);
ZonedDateTime zdt1 = date.atStartOfDay(zone);
  
Instant instant = Instant.now();
ZonedDateTime zdt2 = instant.atZone(zone);
```



## 时间长度
* Duration表示以秒和纳秒为基准的时长。例如，“23.6秒”     <!-- .element: class="fragment" -->
* Period 表示以年、月、日衡量的时长。例如，“3年2个月零6天”     <!-- .element: class="fragment" -->

```java
Period sixMonths = Period.ofMonths(6);
LocalDate date = LocalDate.now();
LocalDate future = date.plus(sixMonths);
```
<!-- .element: class="fragment" -->




## 时钟
```java
// Returns the current time based on your system clock and set to UTC. 
Clock clock = Clock.systemUTC(); 
System.out.println("Clock : " + clock); 

// Returns time based on system clock zone Clock defaultClock = 
Clock.systemDefaultZone(); 
System.out.println("Clock : " + clock); 

Output: 
Clock : SystemClock[Z] 
Clock : SystemClock[Z]
```




## 格式化
* java.time.format   <!-- .element: class="fragment" -->
* DateTimeFormatter和DateTimeFormatterBuilder   <!-- .element: class="fragment" -->
```java
DateTimeFormatter f = DateTimeFormatter.ofPattern("dd/MM/uuuu");
LocalDate date = LocalDate.parse("24/06/2014", f);
String str = date.format(f);
```
<!-- .element: class="fragment" -->



# C/C++中的时间



## 数据结构
* time_t，本质上是一个长整数，表示从1970-01-01 00:00:00到目前计时时间的秒数
* timeval，包含毫秒的数据结构
* tm，存储各个时间字段的结构体



## 定义
```c
struct timeval {
     time_t    tv_sec;     /* seconds */
     suseconds_t  tv_usec; /* microseconds */
 };
```
<!-- .element: class="fragment" -->

```c
struct tm { 
    int tm_sec;   /* seconds after the minute - [0,60] */ 
    int tm_min;   /* minutes after the hour - [0,59] */ 
    int tm_hour;  /* hours since midnight - [0,23] */ 
    int tm_mday;  /* day of the month - [1,31] */ 
    int tm_mon;   /* months since January - [0,11] */ 
    int tm_year;  /* years since 1900 */ 
    int tm_wday;  /* days since Sunday - [0,6] */ 
    int tm_yday;  /* days since January 1 - [0,365] */ 
    int tm_isdst;  /* daylight savings time flag */ 
}; 
```
<!-- .element: class="fragment" -->




## 常用函数
```c
//取得从1970年1月1日至今的秒数 
time_t time(time_t *t); 

//将结构中的信息转换为真实世界的时间，以字符串的形式显示 
char *asctime(const struct tm *tm);

//将timep转换为真是世界的时间，以字符串显示，它和asctime不同就在于传入的参数形式不一样 
char *ctime(const time_t *timep); 

//将time_t表示的时间转换为没有经过时区转换的UTC时间，是一个struct tm结构指针  
struct tm *gmtime(const time_t *timep); 

//和gmtime类似，但是它是经过时区转换的时间。 
struct tm *localtime(const time_t *timep); 

//将struct tm 结构的时间转换为从1970年至今的秒数 
time_t mktime(struct tm *tm); 

//返回当前距离1970年的秒数和微妙数，后面的tz是时区，一般不用 
int gettimeofday(struct timeval *tv, struct timezone *tz); 

//返回两个时间相差的秒数 
double difftime(time_t time1, time_t time2); 
```



# JavaScript中的时间



## Date 对象
```javascript
var myDate = new Date();

myDate.toString();
// "Mon May 08 2017 09:40:49 GMT+0800 (CST)"

myDate.toUTCString();
// "Mon, 08 May 2017 01:40:49 GMT"

myDate.toGMTString();
// "Mon, 08 May 2017 01:40:49 GMT"
```



## moment
* 日期处理库
* Chrome on Windows XP
* IE 8, 9, and 10 on Windows 7
* IE 11 on Windows 10
* latest Firefox on Linux
* latest Safari on OSX 10.8 and 10.11




## moment安装
```npm
npm install moment
```

```javascript
import moment from 'moment';

let now = moment().format('LLLL');
```
<!-- .element: class="fragment" -->

```html
<script src="moment.js"></script>
<script>
    moment().format();
</script>
```
<!-- .element: class="fragment" -->



## moment使用
```javascript
moment();
moment('12-25-1995', 'MM-DD-YYYY');
moment().add(7, 'days').subtract(1, 'months').year(2009).hours(0).minutes(0).seconds(0);

moment().format('dddd, MMMM Do YYYY, h:mm:ss a');
// "Monday, May 8th 2017, 10:10:53 am"

moment.locale('zh-cn');
moment().format('dddd, MMMM Do YYYY, h:mm:ss a');
// "星期一, 五月 8日 2017, 10:13:49 上午"
```



## 时区
* moment-timezone

```npm
npm install moment-timezone
```

```html
<script src="moment.js"></script>
<script src="moment-timezone-with-data.js"></script>
```



## moment-timezone使用
```javascript
moment.tz("2013-12-01", "America/Los_Angeles").format();
// 2013-12-01T00:00:00-08:00
moment.tz("2013-06-01", "America/Los_Angeles").format();
// 2013-06-01T00:00:00-07:00

// Converting to Zone
moment("2013-11-18").tz("America/Toronto").format('Z'); // -05:00
moment("2013-11-18").tz("Europe/Berlin").format('Z');   // +01:00

moment.tz([2012, 0], 'America/New_York').format('z');    // EST
moment.tz([2012, 5], 'America/New_York').format('z');    // EDT

// Default time zone
moment.tz.setDefault('America/New_York');

// Get local zone
moment.defaultZone && moment.defaultZone.name || moment.tz.guess();
// "Asia/Shanghai"

```



## moment 文档
* http://momentjs.com
* http://momentjs.cn



# MySQL中的时间



## 时间类型(MySQL 5.5)
|类型|空间|日期格式|最小值|最大值|零值表示|
|----------|-------|-------|-----|------|------|
|DATETIME |8bytes|YYYY-MM-DD HH:MM:SS|1000-01-01 00:00:00|9999-12-31 23:59:59|0000-00-00 00:00:00|
|TIMESTAMP|4bytes|YYYY-MM-DD HH:MM:SS|1970-01-01 00:00:01|2038-01-19 03:14:07|00000000000000|
|DATE	  |4bytes|YYYY-MM-DD         |1000-01-01         |9999-12-31         |0000-00-00  |
|TIME     |3bytes|HH:MM:SS           |-838:59:59         |838:59:59          |00:00:00    |
|YEAR	  |1bytes|YYYY               |1901               |2155               |0000        |



## 时区支持
```
default-time-zone='timezone'

mysql> SET GLOBAL time_zone = timezone;
mysql> SET time_zone = timezone;
```



# 时间传输
Web <--> Service <--> DB 

**请使用timestamp**



把时间用在思考上是最能节省时间的事情。    
 —— 卡曾斯
