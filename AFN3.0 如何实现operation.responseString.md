# AFN3.0 如何实现operation.responseString

我在AFNetworking issues中的回答[how to get response body in failure block?](https://github.com/AFNetworking/AFNetworking/issues/3551)还有
[How can i get responseString which at AFNetworking 3.0](https://github.com/AFNetworking/AFNetworking/issues/3534)

发现还有好多朋友还不清楚如何实现,其实很简单

```
NSError *underError = error.userInfo[@"NSUnderlyingError"];
NSData *responseData = underError.userInfo[@"com.alamofire.serialization.response.error.data"];
```

有小伙伴问我```com.alamofire.serialization.response.error.data```是怎么来的,原来都是AFJSONResponseSerializer解析修改成```manager.responseSerializer = [AFHTTPResponseSerializer serializer];```这样报错的时候就会看到控制台打印的信息里面有```com.alamofire.serialization.response.error.data```后面输出responseData...然后才有了上面的解决办法

**-----16.6.7更-----**
作者回复中已经添加了相关操作
在```AFURLResponseSerialization```
可以在 failure block 中添加下面代码获取responseString

```
NSData *data = error.userInfo[AFNetworkingOperationFailingURLResponseDataErrorKey];
```

具体代码:

```
/**
 ## User info dictionary keys

 These keys may exist in the user info dictionary, in addition to those defined for NSError.

 - `NSString * const AFNetworkingOperationFailingURLResponseErrorKey`
 - `NSString * const AFNetworkingOperationFailingURLResponseDataErrorKey`

 ### Constants

 `AFNetworkingOperationFailingURLResponseErrorKey`
 The corresponding value is an `NSURLResponse` containing the response of the operation associated with an error. This key is only present in the `AFURLResponseSerializationErrorDomain`.

 `AFNetworkingOperationFailingURLResponseDataErrorKey`
 The corresponding value is an `NSData` containing the original data of the operation associated with an error. This key is only present in the `AFURLResponseSerializationErrorDomain`.
 */
FOUNDATION_EXPORT NSString * const AFNetworkingOperationFailingURLResponseErrorKey;

FOUNDATION_EXPORT NSString * const AFNetworkingOperationFailingURLResponseDataErrorKey;
```

