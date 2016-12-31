容易发现Cocoa Foundation 中提供了一些可变参数的方法，如：
``` Objective-C
NSLog(NSString *format, ...)
```
在实际的编程实践中，我们也需要自己实现可变参数的方法。在Objc中，是依靠原生C库来的实现的。
请看示例：
``` Objective-C
- (void) doLog:(NSString *)formatStr, ... {
    NSMutableArray *arr = [[NSMutableArray alloc]init];
    NSString *arg;
    va_list argList;
    if(formatStr)
    {
        va_start(argList, formatStr);
        while ((arg = va_arg(argList, NSString*)))
        {
            [arr addObject:arg];
        }
        va_end(argList);
    }
    
    for (NSString *str in arr) {
        NSLog(@"%@", str);
    }

}
```

下面就代码段中用的C方法一一说明；

1. va_list argList：定义一个指向个数可变的参数列表指针;
1.  va_start(ap, param)param是第一个可选参数前的固定参数，va_start 使指针指向第一个可选参数;
1. va_arg(ap, type)返回参数列表中指针ap所指的参数，返回类型为type，并使指针ap指向参数列表中下一个参数;
1. va_end(ap) 清空参数列表，并置参数指针ap无效.