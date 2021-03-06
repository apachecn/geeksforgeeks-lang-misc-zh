# Perl–使用正则表达式

从字符串中提取日期

> 原文:[https://www . geesforgeks . org/perl-从字符串中提取日期-使用-regex/](https://www.geeksforgeeks.org/perl-extracting-date-from-a-string-using-regex/)

在 [Perl](https://www.geeksforgeeks.org/introduction-to-perl/) 中，一般我们要读取 CSV(逗号分隔值)文件来提取需要的数据。有时文件名中有日期，如示例 2014-02-12T11:10:10.csv，或者文件中可能有一列有日期。这些日期可以是任何模式，如 **YYYY-MM-DDThh:mm:ss** 或**DD/MM/YYY**T6【hh . MM . SS。处理那些日期；Perl 脚本应该足够灵活，能够处理字符串中不同类型的日期格式。我们需要使用正则表达式特征从字符串中提取日期。正则表达式是定义您正在查看的特定模式的字符串。应用正则表达式的基本方法是使用模式绑定运算符=~和！~.

在 Perl 中，有多个库可用于处理日期和时间，如日期::解析和时间::片段；这两个库都有许多灵活的功能来处理更复杂的需求。但是这些库不是标准 Perl 模块的一部分，您需要单独安装它们。

对于一般的日期格式，不用安装任何新的库就能找到特定的正则表达式。让我们来看一些在 Perl 中从字符串解析日期的例子。

在我们看从字符串中提取日期的例子之前，我们应该看一下在解析字符串中的表达式时使用的这些元符号:

<figure class="table">

| **^** | 元字符匹配字符串的开头 |
| **$** | 元符号匹配字符串的结尾 |
| ***** | 匹配前面表达式的 0 次或更多次出现 |
| **+** | 匹配前面表达式的一次或多次出现 |
| **？** | 匹配前面表达式的 0 或 1 个匹配项 |

</figure>

这里有一些简单的例子。

<figure class="table">

| **/^$/** | #字符串中没有任何内容(开始和结束相邻) |
| **/(\d\s) {3}/** | 三个数字，每个数字后面都有一个空格，例如:6 7 8 |
| **/(a)+/** | 匹配一个字符串，其中每个下一个字母都是 |
| **/^\d+/** | 字符串以一个或多个数字开头 |
| **/\d+$/** | 字符串以一个或多个数字结尾 |

</figure>

正则表达式不需要单独的模块。它内置于 Perl(任何版本)。所以你应该在你的系统上安装 Perl(任何版本)。我们将看到一些使用 Perl 正则表达式从字符串中提取不同格式的日期的例子。

**例 1:**

在这个例子中，我们将看到如何用模式 yyyy-mm-ddThh:mm:ss 从 Perl 的字符串中提取日期。下面的示例 1 显示了一个字符串样本 2018-03-21T12:10:10.csv，我们需要从中提取以年、月和日期为单位的日期变量，以使其可用于进一步的脚本。

这里，正则表达式\d\d\d\d 确保字符串中的日期模式应该以 4 位数字的模式开始。如果没有，那么它会抛出一个未初始化的变量异常，因为字符串中缺少模式。

d 代表什么？/d 的意思是？该模式确保月、日、小时、分钟和秒可以是 1 位数或 2 位数。

**例如:**

2013-9-21T11:3:30

2014-12-3T9:1:10

所以/d？/d 会保证表达式留到**吗？**是可选的，它将毫无错误地执行。

## Perl 语言

```perl
#!/usr/bin/perl
# your code here
my $str = "sample2018-03-21T12:10:10.csv";
my (($year, $month, $day, $hour, $min, $sec) = 
     $str =~ /(\d\d\d\d)-(\d?\d)-(\d?\d)T(\d?\d):(\d?\d):(\d?\d)/);
print "year : $year  month:$month  day:$day - hour:$hour  minute:$min  seconds:$sec\n";
```

**输出:**

```perl
year : 2018  month:03  day:21 - hour:12  minute:10  seconds:10
```

**例 2:**

在这个例子中，我们将看到如何用模式 mm/dd/yyyy hh.mm.ss 从字符串中提取日期。日期可以是文件名的一部分，也可以是内容。因此，下面的示例将有助于从字符串中解析格式为 mm/dd/yyyy hh:mm:ss 的日期。在本例中，我们进行了字符串测试 _ 28/04/2017 11 . 00 . 00；其中日期以 2 位数 28 开头，后跟反斜杠/

这里，(\d？\d) regex 确保字符串以 2 或 1 位后跟/的模式开始。反斜杠\放在。以确保它只匹配点，而不是像通常那样匹配每个字符。

## Perl 语言

```perl
#!/usr/bin/perl
# your code here
my $str1 = "test_28/04/2017 11.00.00";
my (($month1, $day1, $year1, $hour1, $min1, $sec1) = 
     $str1 =~ m{(\d?\d)/(\d?\d)/(\d\d\d\d) (\d\d)\.(\d\d)\.(\d\d)}); 
print "year:$year1  month:$month1  day:$day1 - hour:$hour1  minute:$min1  seconds:$sec1\n";
```

**输出:**

```perl
year:2017  month:28  day:04 - hour:11  minute:00  seconds:00
```

**例 3:**

在这里我们将看到另一个日期模式，即{Day}，dd {mon} yyyy hh:mm:ss，如 2014 年 2 月 11 日星期二 11:01:54+0100(CET)；有时 CSV 文件具有上面格式的日期列值，这对于 Perl 操作来说是不可读的，所以我们希望从这种格式中提取年、月和日期，并根据需要使用它。

给你。+?(\d+) regex 表示日期数字 11 之前会有一些字符，在\s(。+?)regex 的意思是日期后面跟一个空格和字符串，是 Feb，s(\d+)/ regex 确保 11 Feb 后面跟一个空格和多个数字，是 2014。我们将这些值保存在为日、月和年定义的变量中；可以在下一个脚本中使用。

## Perl 语言

```perl
#!/usr/bin/perl
# your code here
my $string = 'Date: Tue, 11 Feb 2014 11:01:57 +0100 (CET)';
my ($day3, $month3, $year3) = $string =~ /Date:.+?(\d+)\s(.+?)\s(\d+)/;
print "Day:$day3 month:$month3 year:$year3\n";
```

**输出:**

```perl
Day:11 month:Feb year:2014
```