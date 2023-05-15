---
title: "常用正则匹配代码片段"
date: 2023-04-04T14:55:38+08:00
# bookComments: false
# bookSearchExclude: false
---

## 匹配字符串

```text
.       匹配任意单个字符（除了换行符）
*       匹配前面的字符零次或多次
+       匹配前面的字符一次或多次
?       匹配前面的字符零次或一次
\d      匹配一个数字字符
\w      匹配一个单字字符（字母、数字或下划线）
\s      匹配一个空白字符（空格、制表符、换行符等）
^       匹配字符串的开头
$       匹配字符串的结尾
[]      匹配方括号中任意一个字符
[^]     匹配不在方括号中的任意一个字符
()      分组，用于提取匹配的部分

这些正则表达式可以灵活组合使用，构成更复杂的匹配规则。例如，^\d{3}-\d{2}-\d{4}$ 可以匹配格式为 xxx-xx-xxxx 的美国社会保险号码，其中 ^\d{3} 匹配三个数字字符作为开头，-\d{2}- 匹配中间的两个数字和横线，\d{4}$ 匹配四个数字字符作为结尾。


\s*     匹配任意数量的空白字符
.*      匹配任意数量的任意字符
^       匹配行的开头
.*      匹配零个或多个任意字符
/       匹配一个斜杠字符
([^/]+) 匹配一个或多个除斜杠之外的字符，并将其捕获在子组中
/src/main/resources/application\.yaml 匹配特定的字符串（需要转义点号）
$       匹配行的结尾

```

## 提取字符串

其中，圆括号表示一个分组，在该分组内使用 [^"]* 匹配任意非双引号字符，然后使用 () 将其包裹，从而提取其中的内容。同时，使用 \s* 匹配任意数量的空白字符，.* 匹配任意数量的任意字符。在Go中，可以使用 regexp 包来进行正则表达式匹配和提取

```go
func TestMatch(t *testing.T) {
	str := `
    @FeignClient( name   = "service1", path="/path/to/service1")
    public interface Service1Client {
        // ...
    }
    `
	re := regexp.MustCompile(`@FeignClient\(\s*name\s*=\s*"([^"]*)".*\)`)
	matches := re.FindStringSubmatch(str)
	if len(matches) > 1 {
		name := matches[1]
		fmt.Println(name)  // 输出结果为：service1
	}
}
```

这里的正则表达式 @FeignClient\("(.*?)"\) 匹配形如 @FeignClient("xxx") 的字符串，其中 .*? 匹配任意字符（非贪婪模式）。
然后，调用 re.FindStringSubmatch 方法来查找符合正则表达式的子字符串。如果找到了匹配项，返回一个切片，其中第一个元素是整个匹配的结果，后面的元素则是正则表达式中括号内的捕获组（如果有的话）。因此，我们可以通过 match[1] 来获取 sc-service-b 这个可变值

```go
str := "@FeignClient(\"sc-service-b\")"
    re := regexp.MustCompile(`@FeignClient\("(.*?)"\)`)
    match := re.FindStringSubmatch(str)
    if len(match) == 2 {
        value := match[1]
        fmt.Println(value)  // 输出：sc-service-b
    }
```

可以使用正则表达式 \/(\w+)\?? 来提取字符串中的 b，其中：
\/ 匹配斜杠 /；
(\w+) 使用括号表示一个分组，匹配一个或多个字母、数字或下划线字符；
\?? 匹配一个可选的问号 ?。

```go
import "regexp"

str1 := "a/b"
str2 := "a/b?u=8"

pattern := `\/(\w+)\??`
reg := regexp.MustCompile(pattern)

match1 := reg.FindStringSubmatch(str1)  // ["\/b", "b"]
match2 := reg.FindStringSubmatch(str2)  // ["\/b?u=8", "b"]

if len(match1) > 1 {
    fmt.Println(match1[1])  // "b"
}

if len(match2) > 1 {
    fmt.Println(match2[1])  // "b"
}
```
