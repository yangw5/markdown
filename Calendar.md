## Calendar

在早期的 JDK 版本中，Date 类附有两大功能：
　　
1. 允许用年、月、日、时、分、秒来解释日期
2. 允许对表示日期的字符串进行格式化和句法分析

在JDK1.1中提供了类 Calendar 来完成第一种功能，类 DateFormat 来完成第二项功能。DateFormat 是 java.text 包中的一个类。与 Date 类有所不同的是，DateFormat 类可以接受用各种语言和不同习惯表示的日期字符串。

但是 Calendar 类是一个抽象类，它完成 Date 类与普通日期表示法之间的转换，而我们更多的是使用 Calendar 类的子类 GregorianCalendar 类。它实现了世界上普遍使用的公历系统。当然我们也可以继承 Calendar 类，然后自己定义实现日历方法。

先来看一看 GregorianCalendar 类的构造函数：

| 构造方法 | 说明 |
|----------|------|
| GregorianCalendar() | 创建的对象中的相关值被设置成指定时区，缺省地点的当前时间，即程序运行时所处的时区、地点的当前时间 |
| GregorianCalendar(TimeZone zone) | 创建的对象中的相关值被设置成指定时区 zone，缺省地点的当前时间 |
| GregorianCalendar(Locale aLocale) | 创建的对象中的相关值被设置成缺省时区，指定地点 aLocale 的当前时间 | 
| GregorianCalendar(TimeZone zone,Locale aLocale) | year - 创建的对象中的相关值被设置成指定时区，指定地点的当前时间 |

TimeZone 是 java.util 包中的一个类，其中封装了有关时区的信息。每一个时区对应一组 ID。类 TimeZone 提供了一些方法完成时区与对应 ID 两者之间的转换。

例如：
```java
//太平洋时区的 ID 为 PST
TimeZone tz0 = TimeZone.getTimeZone("PST")
//getDefault()可以获取主机所处时区的对象
TimeZone tz1 = TimeZone.getDefault()
```

Locale 只是一种机制，它用来标识一个特定的地理、政治或文化区域获取一个 Locale 对象的构造方法：

```java
//调用Locale类的构造方法
Locale l0 = new Locale(String language)
Locale l1 = new Locale(String language, String country)
Locale l2 = new Locale(String languge, String country, String variant)

//调用Locale类中定义的常量
Locale  l1 = Locale.CHINA
```

### Calendar 编程实例

在`/home/project/`目录下新建源代码文件`CalendarDemo.java`。

```java
import java.text.DateFormat;
import java.text.SimpleDateFormat;
import java.util.Calendar;
import java.util.Date;

public class CalendarDemo {
    public static void main(String[] args) {
        System.out.println("完整显示日期时间：");
        // 字符串转换日期格式
        DateFormat fdate = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        String str = fdate.format(new Date());
        System.out.println(str);

        // 创建 Calendar 对象
        Calendar calendar = Calendar.getInstance();
        // 初始化 Calendar 对象，但并不必要，除非需要重置时间
        calendar.setTime(new Date());

        // 显示年份
        System.out.println("年： " + calendar.get(Calendar.YEAR));

        // 显示月份 (从0开始, 实际显示要加一)
        System.out.println("月： " + calendar.get(Calendar.MONTH));


        // 当前分钟数
        System.out.println("分钟： " + calendar.get(Calendar.MINUTE));

        // 今年的第 N 天
        System.out.println("今年的第 " + calendar.get(Calendar.DAY_OF_YEAR) + "天");

        // 本月第 N 天
        System.out.println("本月的第 " + calendar.get(Calendar.DAY_OF_MONTH) + "天");

        // 3小时以后
        calendar.add(Calendar.HOUR_OF_DAY, 3);
        System.out.println("三小时以后的时间： " + calendar.getTime());
        // 格式化显示
        str = (new SimpleDateFormat("yyyy-MM-dd HH:mm:ss:SS")).format(calendar.getTime());
        System.out.println(str);

        // 重置 Calendar 显示当前时间
        calendar.setTime(new Date());
        str = (new SimpleDateFormat("yyyy-MM-dd HH:mm:ss:SS")).format(calendar.getTime());
        System.out.println(str);

        // 创建一个 Calendar 用于比较时间
        Calendar calendarNew = Calendar.getInstance();

        // 设定为 5 小时以前，后者大，显示 -1
        calendarNew.add(Calendar.HOUR, -5);
        System.out.println("时间比较：" + calendarNew.compareTo(calendar));

        // 设定7小时以后，前者大，显示 1
        calendarNew.add(Calendar.HOUR, +7);
        System.out.println("时间比较：" + calendarNew.compareTo(calendar));

        // 退回 2 小时，时间相同，显示0
        calendarNew.add(Calendar.HOUR, -2);
        System.out.println("时间比较：" + calendarNew.compareTo(calendar));

        // calendarNew创建时间点
        System.out.println((new SimpleDateFormat("yyyy-MM-dd HH:mm:ss:SS")).format(calendarNew.getTime()));
        // calendar创建时间点
        System.out.println((new SimpleDateFormat("yyyy-MM-dd HH:mm:ss:SS")).format(calendar.getTime()));
        System.out.println("时间比较：" + calendarNew.compareTo(calendar));
    }
}
```
编译运行：
```bash
$ javac CalendarDemo.java
$ java CalendarDemo
完整显示日期时间：
2018-12-12 15:50:49
年： 2018
月： 11
分钟： 50
今年的第 346天
本月的第 12天
三小时以后的时间： Wed Dec 12 18:50:49 CST 2018
2018-12-12 18:50:49:449
2018-12-12 15:50:49:455
时间比较：-1
时间比较：1
时间比较：1
2018-12-12 15:50:49:456
2018-12-12 15:50:49:455
时间比较：1
```

大家运行上面的代码后，看见控制台上的输出结果会不会有所疑问呢？

其实 month 的含义与 Date 类相同，0 代表 1 月，11 代表 12 月。

有的同学可能不明白最后一个的输出为什么有时是 0 ，有时是 1，在这里会涉及到 calendarNew 与 calendar 的创建时间点， calendarNew 经过增加和减少时间后恢复到原来的时间点，也就是最终比较的是谁先创建好，时间点靠后的大一些，而 calendarNew 创建的时间点只有可能是大于等于 calendar 的，需要根据实际的创建时间点进行比较。

```checker
- name: 检查是否存在 CalendarDemo 
  script: |
    #!/bin/bash
    ls /home/project/CalendarDemo.java
  error: |
    没有找到 /home/project/CalendarDemo.java 文件
```