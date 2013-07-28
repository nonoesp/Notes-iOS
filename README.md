iOS-Notes
=========

A personal guide with notes of Cocoa for iOS.


## Status Bar

```objc
// Show and hide
[[UIApplication sharedApplication] setStatusBarHidden:(BOOL) withAnimation:(UIStatusBarAnimation)];
```

**UIStatusBarAnimation values**
* UIStatusBarAnimationFade
* UIStatusBarAnimationSlide
* UIStatusBarAnimationNone


## NSTimer

```objc
NSTimer *timer = [NSTimer timerWithTimeInterval:(float) target:self selector:@selector(someMethod) userInfo:nil repeats:(BOOL)];
[[NSRunLoop mainRunLoop] addTimer:timer forMode:NSDefaultRunLoopMode];
```

*If someMethod takes arguments the selector name would be @selector(someMethod:)*