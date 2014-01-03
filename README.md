BZGFormViewController
=====================

BZGFormViewController is a library for making dynamic forms.

![alt tag](https://raw.github.com/benzguo/BZGFormViewController/master/Screenshots/SignupForm.gif)

## Demo app
Navigate to /SignupForm, run `pod install`, and open `SignupForm.xcworkspace` to see the dynamic signup form used to make the above gif.

## Installation

Cocoapods recommended. You can also copy the contents of /BZGFormViewController into your project.

## Overview

+ **BZGFormFieldCell**
    + A `UITableViewCell` subclass for displaying form fields.
+ **BZGFormInfoCell**
    + A `UITableViewCell` subclass for displaying form field info. Each form field cell has a corresponding info cell.
+ **BZGFormViewController**
    + A `UITableViewController` subclass that handles the display of field cells and info cells.

## Quick start

First, subclass `BZGFormViewController`.

```objective-c
@interface SignupViewController : BZGFormViewController
```

Next, import "BZGFormFieldCell.h" and create a cell.

```objective-c
#import "BZGFormFieldCell.h"

// ...

self.usernameFieldCell = [BZGFormFieldCell new];
self.usernameFieldCell.label.text = @"Username";
self.usernameFieldCell.textField.placeholder = @"Username";
self.usernameFieldCell.textField.keyboardType = UIKeyboardTypeASCIICapable;
```

To validate text, first register as a delegate of the text field.

```objective-c
self.usernameFieldCell.textField.delegate = self;
```

To validate the text and update the form when the text field's text changes, use the cell's `shouldChangeTextBlock`

```objective-c
self.usernameFieldCell.shouldChangeTextBlock = ^BOOL(BZGFormFieldCell *cell, NSString *newText) {
    if (newText.length < 5) {
        cell.validationState = BZGValidationStateInvalid;
        [cell.infoCell setText:@"Username must be at least 5 characters long."];
        cell.shouldShowInfoCell = YES;
    } else {
        cell.validationState = BZGValidationStateValid;
        cell.shouldShowInfoCell = NO;
    }
    return YES;
};
    








