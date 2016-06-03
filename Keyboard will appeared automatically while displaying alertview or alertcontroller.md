# Keyboard will appeared automatically while displaying alertview or alertcontroller

>[stackoverflow](http://stackoverflow.com/questions/30498972/keyboard-will-appeared-automatically-in-ios-8-3-while-displaying-alertview-or-al)

我采用其中

```
 [YOUR_TEXT resignFirstResponder];
            dispatch_after(dispatch_time(DISPATCH_TIME_NOW, (int64_t)(.6 * NSEC_PER_SEC)), dispatch_get_main_queue(), ^{


                    _alertVw = [[UIAlertView alloc] initWithTitle:@"" message:@"message." delegate:self cancelButtonTitle:@"Ok" otherButtonTitles:nil, nil];

                    [_alertVw show];
});

```
这种方案解决的


