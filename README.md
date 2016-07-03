# SGGestureRecognizer

SGGestureRecognizer is a graphics gesture recognizer based on Dollar One Alghrithm for iOS. It's more powerful than the UIGestureRecognizeer, it can record any gesture graphic at one stroke, suck as a star, an rectangle and so on. You can use these graphics to execute specific action.

## A GIF about the Recognizer
<p>
<img src="https://raw.githubusercontent.com/Soulghost/SGGestureRecognizer/master/images/recognize.gif" width = "300" height = "533" alt="WiFi Page" align=center />
</p>

## How To Get Started
- [Download SGGestureRecognizer](https://github.com/Soulghost/SGGestureRecognizer/archive/master.zip) and try out the inclued iPhone example app.

## Installation
Drag the `SGGestureRecognizer` folder to your project.

## Usage
### Import header
```objective-c
#import "SGGestureRecognizer.h"
```

### Add a gesture
Firstly, you should sample some points on the gesture path and put them to an `NSArray`, such as `NSMutableArray<NSValue *> *samplePoints`, for recognize, you should name the gesture when you create a gesture set.
```objective-c
SGDollarOneManager *mgr = [SGDollarOneManager sharedManager];
SGGestureSet *set = [SGGestureSet gestureSetWithName:<name of the gesture> points:self.samplePoints];
if (set.countPoints) {
    [mgr addGestureSet:set];
}
```

### Recognize a gesture
You also should sample some points on the gesture path and pass to `SGGestureSet`, the recognizer will standardize the set and generate vector to compare with the vectors in gesture library.
```objective-c
SGDollarOneManager *mgr = [SGDollarOneManager sharedManager];
SGGestureSet *set = [SGGestureSet gestureSetWithPoints:self.samplePoints];
NSString *gesName = [mgr recognizeGestureSet:set];
```
if the gesName is not nil, that means the gesture is recognize succeeded.

### Preview and delete gestures in library
You can preview and delete gestures in library by present an `SGGesturePreviewController` embedded in an `UINavigationController`.
```objective-c
- (void)preview {
    SGGesturePreviewController *vc = [[SGGesturePreviewController alloc] init];
    UINavigationController *nav = [[UINavigationController alloc] initWithRootViewController:vc];
    [self presentViewController:nav animated:YES completion:nil];
}
```
The `SGGesturePreviewController` will load gestures from the `SGGestureManager`, you can delete a gesture by slide left a gesture cell.

### Modify the library path
You can customize the gesture library save and load path by change the property in `SGGestureManager`.
The coed below change the load path to main bundle, when you change the load path, the manager will reload gestures from the new path.
```objective-c
[SGDollarOneManager sharedManager].libLoadPath = [[NSBundle mainBundle] pathForResource:@"gestureLib.gs" ofType:nil];
```
The save path is the Caches Directory by default.
