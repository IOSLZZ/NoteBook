#iOS 判断设备是否安装SIM卡
>http://stackoverflow.com/questions/10488898/iphone-detecting-sim-card-availability

```
#import <CoreTelephony/CTTelephonyNetworkInfo.h> 
#import <CoreTelephony/CTCarrier.h>
```


```
/// 判断设备是否安装sim卡
+(BOOL)isSIMInstalled
{
    CTTelephonyNetworkInfo *networkInfo = [[CTTelephonyNetworkInfo alloc] init];
    CTCarrier *carrier = [networkInfo subscriberCellularProvider];
    if (!carrier.isoCountryCode) {
        NSLog(@"No sim present Or No cellular coverage or phone is on airplane mode.");
        return NO;
    }
    return YES;
}

```


