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


##NSUserDefaults

Class types of objects which can be stored in NSUserDefaults:

* NSData
* NSString
* NSNumber
* NSDate
* NSArray
* NSDictionary


```objc
// Get the shared instance of User Defaults
NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];

// Set object for key
[defaults setObject:(id) forKey:@"PROPERTY_KEY"];

// Retrieve object with key
[defaults objectForKey:@"PROPERTY_KEY"];

// If the object is an NSString
NSString *firstName = [defaults objectForKey:@"PROPERTY_KEY"];
```