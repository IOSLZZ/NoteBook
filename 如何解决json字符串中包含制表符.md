# 如何解决json字符串中包含制表符
错误信息:

```
Error Domain=NSCocoaErrorDomain Code=3840 "The operation couldn’t be completed. (Cocoa error 3840.)" (Unescaped control character around character 135.) UserInfo=0x170e79d00 {NSDebugDescription=Unescaped control character around character 135.}
```

如何处理:
最关键的地方:

```
-(NSString *)removeUnescapedCharacter:(NSString *)inputStr
{
    NSCharacterSet *controlChars = [NSCharacterSet controlCharacterSet];//获取那些特殊字符
    NSRange range = [inputStr rangeOfCharacterFromSet:controlChars];//寻找字符串中有没有这些特殊字符
    if (range.location != NSNotFound)
        {
        NSMutableString *mutable = [NSMutableString stringWithString:inputStr];
        while (range.location != NSNotFound)
            {
            [mutable deleteCharactersInRange:range];//去掉这些特殊字符
            range = [mutable rangeOfCharacterFromSet:controlChars];
            }
        return mutable;
        }
    return inputStr;
}

```

举例:

```

    NSString *responseString = [NSMutableString stringWithString:[request responseString]];
    responseString =[self removeUnescapedCharacter:responseString];
    NSData *jsonData = [responseString dataUsingEncoding:NSUTF8StringEncoding];
    NSError *error;
    NSDictionary * dic = [NSJSONSerialization JSONObjectWithData:jsonData options:0 error:&error];
    
```





