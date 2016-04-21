# 修改textField的placeholder的字体颜色、大小

最简单的方法是使用KVC

```
	textField.placeholder = @"placeholder";  
	[textField setValue:[UIColor redColor] forKeyPath:@"_placeholderLabel.textColor"];  
	[textField setValue:[UIFont boldSystemFontOfSize:16] forKeyPath:@"_placeholderLabel.font"];  

```

