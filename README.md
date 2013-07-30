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

Some 

##NSUserDefaults

*A programmatic interface for interacting with the defaults system.* You can store default objects of the following classes: *NSData, NSString, NSNumber, NSDate, NSArray or NSDictionary.* Any other types should be wrapped within an NSData object.


```objc
// Get the shared instance of User Defaults
NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];

// Set object for key
[defaults setObject:(id) forKey:@"PROPERTY_KEY"];

// Retrieve object with key
[defaults objectForKey:@"PROPERTY_KEY"];
```

Example to store and retrieve an NSString
```objc
// Store a name and last name
[defaults setObject:@"Steve" forKey:@"firstName"];
[defaults setObject:@"Jobs" forKey:@"lastName"];

// Retrieving defaults
NSString *firstName = [defaults objectForKey:@"firstName"];
NSString *lastName = [defaults objectForKey:@"lastName"];
```

## AppDelegate

Access the shared Application Delegate instance.

```objc
// Get shared instance of AppDelegate to access properties and methods
AppDelegate *appDelegate = (AppDelegate*)[[UIApplication sharedApplication] delegate];

// If AppDelegate implements the method someMethod
[appDelegate someMethod];

// If AppDelegate has a property call aString
NSString *aString = [appDelegate aString];
```

## Shortcuts

A list of useful shortcuts to navigate the user interface of Xcode faster.

* `FN + left-arrow / right-arrow`
Scroll to the top or bottom of the file.

