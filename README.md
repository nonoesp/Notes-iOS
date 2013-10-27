iOS-Notes
=========

A personal guide with notes of Cocoa, iOs and Xcode.

## Table of Contents

* References
* Libraries
* Guide
* Xcode Shortcuts

## References

* [NYTimes Objective-C Style Guide](https://github.com/NYTimes/objective-c-style-guide)

## Libraries

*Useful libraries and their respective pods for [CocoaPods](http://cocoapods.org) if existent.*

* [UnitsKit](https://github.com/stevemoser/UnitsKit) `pod 'UnitsKit', '~> 0.0.1'`
* [NoticeView](https://github.com/tciuro/NoticeView) `pod 'NoticeView', '~> 3.0.7'`
* [DB5](https://github.com/quartermaster/DB5) `pod 'DB5', '~> 0.0.1'`
* [BlocksKit](https://github.com/pandamonia/BlocksKit) `pod 'BlocksKit', '~> 1.8.3'`
* [MMMarkdown](https://github.com/mdiep/MMMarkdown) `pod 'MMMarkdown', '~> 0.2.3'`
* [SSToolkit](https://github.com/soffes/sstoolkit) `pod 'SSToolkit', '~> 1.0.4'`

*platform :ios, '7.0'

## Guide

### Status Bar

```objc
// Show and hide
[[UIApplication sharedApplication] setStatusBarHidden:(BOOL) withAnimation:(UIStatusBarAnimation)];
```

**UIStatusBarAnimation values**
* UIStatusBarAnimationFade
* UIStatusBarAnimationSlide
* UIStatusBarAnimationNone


### NSTimer

```objc
NSTimer *timer = [NSTimer timerWithTimeInterval:(float) target:self selector:@selector(someMethod) userInfo:nil repeats:(BOOL)];
[[NSRunLoop mainRunLoop] addTimer:timer forMode:NSDefaultRunLoopMode];
```

*If someMethod takes arguments the selector name would be @selector(someMethod:)*

```objc
// Invalidate the timer (stop)
[timer invalidate];
timer = nil;
```

Some 

### NSUserDefaults

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

### AppDelegate

Access the shared Application Delegate instance.

```objc
// Get shared instance of AppDelegate to access properties and methods
AppDelegate *appDelegate = (AppDelegate*)[UIApplication sharedApplication].delegate;

// If AppDelegate implements the method someMethod
[appDelegate someMethod];

// If AppDelegate has a property call aString
NSString *aString = [appDelegate aString];
```

### NSLog

Logging on the console.

```objc
// NSLog an NSString
NSLog(@"Hello World!");

// NSLog a formatted NSString
NSLog(@"My name is %@", @"Steve");

// NSLog formatted NSString depending on a boolean value
NSLog(@"%@", isActive ? @"YES" : @"NO");
```

### Touches

For implementation in touchesBegan, touchesMoved, touchesEnded methods.

```objc
UITouch *touch = [touches anyObject];

// Create a CGPoint (x, y) with touch position relative to a current view
CGPoint touchPoint = [touch locationInView:self];

// Get coordinate x
CGFloat x = touchPoint.x;
```

### Views

#### ContentMode

```objc
// Create a UIImageView
UIImageView *imageContainer = [[UIImageView alloc] initWithFrame:CGRectMake(0.0, 0.0, 100.0, 100.0)];

// Set the image property
UIImage *myImage = [UIImage imageNamed:@"image.png"];

// Set the contentMode to fit the image; same result than CSS background-size:cover;
imageContainer.contentMode = UIViewContentModeScaleAspectFit;
```
### Incrementing an int

```objc
// Define an int
int age = 20;

// Increase its value 2
age += 2; // returns 22
```

## Xcode Shortcuts

A list of useful shortcuts to navigate the user interface of Xcode faster.

* `FN + left-arrow / right-arrow` Scroll to the top or bottom of the file.

* `FN + top-arrow / down-arrow` Scroll up or down faster.

* `CTRL + L` Positions the line in edition on the middle of the screen.

* `CMD + 0` Show/hide the File Inspector.

* `CMD + SHIFT + 2` Organizer



