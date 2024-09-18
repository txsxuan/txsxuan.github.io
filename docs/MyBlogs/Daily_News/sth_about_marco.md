# 关于宏
> `本篇记于2024.8.31`<br />

有幸见识到了几种可以用于判断宏是否被定义的方法，摘自stackflow论坛,[这里是原链接](https://stackoverflow.com/questions/26099745/test-if-preprocessor-symbol-is-defined-inside-macro)
1. 直接比较宏本身字符串化后的结果和宏名称字符串化的结果（ps:如果宏没有被定义，二者肯定相等，否则大概率返回不相等）
``` cpp
#include <iostream>
#include <cstring>

#define TRACE_STRINGIFY(item) "" #item
#define TRACE(macro, message)                          \
    do {                                               \
        if (strcmp("" #macro, TRACE_STRINGIFY(macro))) \
            std::cout << message << "\n";              \
    } while (0)
```
其中 __""__ __#item__ 表示将参数item先字符串化，再加上一个空字符串的前缀。

2. 采用
``` cpp
#define __ARG_PLACEHOLDER_1 0,
#define __take_second_arg(__ignored, val, ...) val

/*
 * Helper macros to use CONFIG_ options in C/CPP expressions. Note that
 * these only work with boolean and tristate options.
 */

/*
 * Getting something that works in C and CPP for an arg that may or may
 * not be defined is tricky.  Here, if we have "#define CONFIG_BOOGER 1"
 * we match on the placeholder define, insert the "0," for arg1 and generate
 * the triplet (0, 1, 0).  Then the last step cherry picks the 2nd arg (a one).
 * When CONFIG_BOOGER is not defined, we generate a (... 1, 0) pair, and when
 * the last step cherry picks the 2nd arg, we get a zero.
 */
#define __is_defined(x)         ___is_defined(x)
#define ___is_defined(val)      ____is_defined(__ARG_PLACEHOLDER_##val)
#define ____is_defined(arg1_or_junk)    __take_second_arg(arg1_or_junk 1, 0)
```