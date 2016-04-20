Notes-iOS
=========

A personal guide with notes of Cocoa, iOs and Xcode.

Code snippets appear in both Swift and Objective-C.


## Table of Contents

* References
* Libraries
* Guide
* Xcode Shortcuts
* Errors

## References

* [NYTimes Objective-C Style Guide](https://github.com/NYTimes/objective-c-style-guide)
* [Advances in OpenGL ES 3.0](https://developer.apple.com/videos/play/techtalks-ios-7/10/) (Apple iOS 7 Tech Talks)

## Libraries

*Useful libraries and their respective pods for [CocoaPods](http://cocoapods.org) if existent.*

* [AFNetworking](https://github.com/AFNetworking/AFNetworking) `pod 'AFNetworking', '~> 2.2.0'`
* [UnitsKit](https://github.com/stevemoser/UnitsKit) `pod 'UnitsKit', '~> 0.0.1'`
* [NoticeView](https://github.com/tciuro/NoticeView) `pod 'NoticeView', '~> 3.0.7'`
* [DB5](https://github.com/quartermaster/DB5) `pod 'DB5', '~> 0.0.1'`
* [BlocksKit](https://github.com/pandamonia/BlocksKit) `pod 'BlocksKit', '~> 1.8.3'`
* [MMMarkdown](https://github.com/mdiep/MMMarkdown) `pod 'MMMarkdown', '~> 0.2.3'`
* [SSToolkit](https://github.com/soffes/sstoolkit) `pod 'SSToolkit', '~> 1.0.4'`
* TestFlightSDK `pod 'TestFlightSDK', '~> 2.0.1'` (need to manually download and drag libTestFlight.a to its Pod's target Build Phases > )
* [IonIcons](https://github.com/TapTemplate/ionicons-iOS) `pod 'ionicons'`
* [FLKAytoLayout](https://github.com/dkduck/FLKAutoLayout) `pod 'FLKAutoLayout', '~> 0.1.1'`

*platform :ios, '8.2'

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

Objective-C
```objc
// NSLog an NSString
NSLog(@"Hello, World!");

// NSLog a formatted NSString
NSLog(@"My name is %@", @"Steve");

// NSLog formatted NSString depending on a boolean value
NSLog(@"%@", isActive ? @"YES" : @"NO");
```

Swift

```swift
// println String
println("Hello, World")
```

### Formatting Numbers

```objc
NSString *time = [NSString stringWithFormat:@"%02i:%02i", hours, minutes];
```

### Touches

For implementation in touchesBegan, touchesMoved, touchesEnded methods.

Objective-C

```objc
UITouch *touch = [touches anyObject];

// Create a CGPoint (x, y) with touch position relative to a current view
CGPoint touchPoint = [touch locationInView:self];

// Get coordinate x
CGFloat x = touchPoint.x;
```

Swift

```swift
// Get the CGPoint using Swift
let touch = (touches.first as! UITouch)
let touchPoint = touch.locationInView(self.view)

// A more compressed way
let touchPoint = (touches.first as! UITouch).locationInView(self.view)
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

### Save and load an image
```objc
- (IBAction)saveImage:(UIImage*)image {
    NSArray *paths = NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES);
    NSString *documentsDirectory = [paths objectAtIndex:0];
    NSString *savedImagePath = [documentsDirectory stringByAppendingPathComponent:@"savedImage.png"];
    NSData *imageData = UIImagePNGRepresentation(image);
    [imageData writeToFile:savedImagePath atomically:NO];
}

- (UIImage*)getImageWithName:(NSString*)imageName {
    NSArray *paths = NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES);
    NSString *documentsDirectory = [paths objectAtIndex:0];
    NSString *getImagePath = [documentsDirectory stringByAppendingPathComponent:imageName];
    UIImage *img = [UIImage imageWithContentsOfFile:getImagePath];
    return img;
}
```

### Display Markdown Text from file
Requires MMMardown library loaded

```objc
NSString *markdown = [NSString stringWithContentsOfFile:[[NSBundle mainBundle] pathForResource:@"MyMarkdownFile" ofType:@"md"]  encoding:NSUTF8StringEncoding error:nil];
NSString *html = [MMMarkdown HTMLStringWithMarkdown:markdown error:nil];
NSDictionary *options = @{NSDocumentTypeDocumentAttribute: NSHTMLTextDocumentType};
        
NSError *error;
NSAttributedString *preview = [[NSAttributedString alloc] initWithData:[html dataUsingEncoding:NSUTF8StringEncoding] options:options documentAttributes:nil error:&error];

UITextView *liveView = [[UITextView alloc] init];
liveView.attributedText = preview;
```

### Capture An Image From A UIView

```objc
- (UIImage *)captureScreenInRect:(CGRect)captureFrame {
    CALayer *layer;
    layer = self.view.layer;
    UIGraphicsBeginImageContext(self.view.bounds.size);
    CGContextClipToRect (UIGraphicsGetCurrentContext(),captureFrame);
    [layer renderInContext:UIGraphicsGetCurrentContext()];
    UIImage *screenImage = UIGraphicsGetImageFromCurrentImageContext();
    UIGraphicsEndImageContext();
    return screenImage;
}
// source: http://bit.ly/1ebnWo0
```

### Saving UIImage(s) to the Saved Photos Album

After getting the UIImage, the image can be saved to the Camera Roll. The following code automatically asks the user to access the Photo Library and save.

```objc
UIImageWriteToSavedPhotosAlbum([self captureScreenInRect:CGRectMake(0, 0, self.view.frame.size.width, self.view.frame.size.height)], nil, nil, nil);
```

We can also fill the second and third parameters *–id completionTarget and SEL completionSelector.* This, will perform an action whenever the image has finished saving, as the function is asynchronous.

```objc
UIImageWriteToSavedPhotosAlbum(myImage, self, @selector(image:didFinishSavingWithError:contextInfo:), nil);
```

Then, we can implement that method:

```objc
- (void) image: (UIImage *) image didFinishSavingWithError: (NSError *) error contextInfo: (void *) contextInfo {
NSLog(@"The image was saved to the Photo Album.");
}
```

### Find Files From Documents Folder
```objc
-(NSArray *)findFilesWithExtension:(NSString *)extension{
    
    NSMutableArray *matches = [[NSMutableArray alloc]init];
    NSFileManager *fManager = [NSFileManager defaultManager];
    NSString *item;
    NSArray *contents = [fManager contentsOfDirectoryAtPath:[NSHomeDirectory() stringByAppendingPathComponent:@"Documents"] error:nil];
    
    for (item in contents){
        if ([[item pathExtension] isEqualToString:extension]) {
            [matches addObject:item];
        }
    }
    return matches;
}
```

### Get An UIImage From Documents Folder With A Given Name
```objc
-(UIImage*)imageWithName:(NSString*)imageName {
    NSArray *paths = NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES);
    NSString *filePath = [[paths objectAtIndex:0] stringByAppendingPathComponent:imageName];
    UIImage *image = [[UIImage alloc] initWithContentsOfFile:filePath];
    return image;
}
```
### Encode Strings With base64

```objc
NSString *string = @"mySecretString";
NSString *base64EncodedString = [[string dataUsingEncoding:NSUTF8StringEncoding] base64EncodedStringWithOptions:0];

NSLog(@"%@", base64EncodedString); // bXlTZWNyZXRTdHJpbmc=
```

### Force UIWebView to Open Links with Safari

```objc
-(BOOL) webView:(UIWebView *)inWeb shouldStartLoadWithRequest:(NSURLRequest *)inRequest navigationType:(UIWebViewNavigationType)inType {
    if ( inType == UIWebViewNavigationTypeLinkClicked ) {
        [[UIApplication sharedApplication] openURL:[inRequest URL]];
        return NO;
    }
    
    return YES;
}
```

## Xcode Shortcuts

A list of useful shortcuts to navigate the user interface of Xcode faster.

* `FN + left-arrow / right-arrow` Scroll to the top or bottom of the file.

* `FN + top-arrow / down-arrow` Scroll up or down faster.

* `CTRL + L` Positions the line in edition on the middle of the screen.

* `CMD + 0` Show/hide the File Inspector.

* `CMD + SHIFT + 2` Organizer

## Errors

Some errors I found on my way, and somehow managed to solve—because they will happen again in the future.

### CocoaPods 'OBJC_LDFLAGS'

After running 'pod update,' CocoaPods suggest that *Other Linker Flags* has some invalid values.

Removed extra *Library Search Paths* in Build Settings and left only $(inherited).

## License

Notes-iOS is licensed under the MIT license. (http://opensource.org/licenses/MIT)

## Me

I tweet at [@nonoesp](http://www.twitter.com/nonoesp) and write at [nono.ma/says](http://nono.ma/says). I would love to hear about it if you find these notes are useful. Thanks!
