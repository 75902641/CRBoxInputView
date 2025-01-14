<a id="Header_Start"></a> ![CRBoxInputViewHeadImg.png](/ReadmeResources/HeadImg.png "CRBoxInputViewHeadImg.png")
[![CI Status](https://img.shields.io/travis/CRAnimation/CRBoxInputView.svg?style=flat)](https://travis-ci.org/CRAnimation/CRBoxInputView)
[![Version](https://img.shields.io/cocoapods/v/CRBoxInputView.svg?style=flat)](https://cocoapods.org/pods/CRBoxInputView)
[![License](https://img.shields.io/cocoapods/l/CRBoxInputView.svg?style=flat)](https://cocoapods.org/pods/CRBoxInputView)
[![Platform](https://img.shields.io/cocoapods/p/CRBoxInputView.svg?style=flat)](https://cocoapods.org/pods/CRBoxInputView)


### [中文文档](https://github.com/CRAnimation/CRBoxInputView#Header_Start) [/ English Document](https://github.com/CRAnimation/CRBoxInputView/blob/master/README_en.md#Header_Start)


## Feature
-  Support verify code auto fill in iOS12
-  Support `Masonry`
-  Support security type
-  Support custom security image / view
-  Support iOS8  and over

> You can use this widget for verify code, password input or phone number input.<br/>I hope you can like this!


## Critical Updates!!!
We can config custom view, not need to throw the inherit way from the version 1.1.3. You can config custom view with block in `CRBoxInputCellProperty`.
``` objc
customSecurityViewBlock //Custom security view
customLineViewBlock     //Custom line
configCellShadowBlock   //Custom shadow
```
>This update compatibility with the earlier version


## Installation

CRBoxInputView is available through [CocoaPods](https://cocoapods.org). To install
it, simply add the following line to your Podfile:

```ruby
pod 'CRBoxInputView', '1.1.3'
```


## Example

To run the example project, clone the repo, and run `pod install` from the Example directory first.
![iPhone 8 Copy 2.png](/ReadmeResources/ScreenShoot2.png "iPhone 8 Copy 2.png")


## Quick Guide
| Type  | Image |
| :-------------: | :-------------: |
| [Base](#Anchor_Base) | ![Normal.png](/ReadmeResources/1Normal.png "Normal.png")  |
| [Placeholder](#Anchor_Placeholder) | ![Placeholder.png](/ReadmeResources/Add1_Placeholder0.png "Placeholder.png")  |
| [CustomBox](#Anchor_CustomBox)  | ![CustomBox.png](/ReadmeResources/2CustomBox.png "CustomBox.png")  |
| [Line](#Anchor_Line)  | ![Line.png](/ReadmeResources/3Line.png "Line.png")  |
| [SecretSymbol](#Anchor_SecretSymbol)  | ![SecretSymbol.png](/ReadmeResources/4SecretSymbol.png "SecretSymbol.png")  |
| [SecretImage](#Anchor_SecretImage)  | ![SecretImage.png](/ReadmeResources/5SecretImage.png "SecretImage.png")  |
| [SecretView](#Anchor_SecretView)  | ![SecretView.png](/ReadmeResources/6SecretView.png "SecretView.png") |

## Usage

### <a id="Anchor_Base"></a>Base
![Normal.png](/ReadmeResources/1Normal.png "Normal.png")
``` objc
CRBoxInputView *boxInputView = [[CRBoxInputView alloc] initWithFrame:CGRectMake(0, 0, 200, 50)];
boxInputView.codeLength = 4;
boxInputView.keyBoardType = UIKeyboardTypeNumberPad;
[boxInputView loadAndPrepareViewWithBeginEdit:YES]; // BeginEdit: If need begin edit.
[self.view addSubview:boxInputView];

// Get value
// func1, call back block when input text did change
boxInputView.textDidChangeblock = ^(NSString *text, BOOL isFinished) {
    NSLog(@"text:%@", text);
};
// func2, normal readonly property
NSLog(@"textValue:%@", boxInputView.textValue);

// Clear all
[boxInputView clearAllWithBeginEdit:YES]; // BeginEdit: If need begin edit after clear all.

```


<br/>

### <a id="Anchor_Placeholder"></a>Placeholder
![Placeholder.png](/ReadmeResources/Add1_Placeholder0.png "Placeholder.png")
``` objc
CRBoxInputCellProperty *cellProperty = [CRBoxInputCellProperty new];
cellProperty.cellPlaceholderTextColor = [UIColor colorWithRed:114/255.0 green:116/255.0 blue:124/255.0 alpha:0.3]; //optional
cellProperty.cellPlaceholderFont = [UIFont systemFontOfSize:20]; //optional

CRBoxInputView *boxInputView = [CRBoxInputView new];
boxInputView.ifNeedCursor = NO; //optional
boxInputView.placeholderText = @"露可娜娜"; //required
boxInputView.customCellProperty = cellProperty;
[boxInputView loadAndPrepareViewWithBeginEdit:YES];
```


<br/>

### <a id="Anchor_CustomBox"></a>CustomBox
![CustomBox.png](/ReadmeResources/2CustomBox.png "CustomBox.png")
``` objc
CRBoxInputCellProperty *cellProperty = [CRBoxInputCellProperty new];
cellProperty.cellBgColorNormal = color_FFECEC;
cellProperty.cellBgColorSelected = [UIColor whiteColor];
cellProperty.cellCursorColor = color_master;
cellProperty.cellCursorWidth = 2;
cellProperty.cellCursorHeight = 30;
cellProperty.cornerRadius = 4;
cellProperty.borderWidth = 0;
cellProperty.cellFont = [UIFont boldSystemFontOfSize:24];
cellProperty.cellTextColor = color_master;
cellProperty.configCellShadowBlock = ^(CALayer * _Nonnull layer) {
    layer.shadowColor = [color_master colorWithAlphaComponent:0.2].CGColor;
    layer.shadowOpacity = 1;
    layer.shadowOffset = CGSizeMake(0, 2);
    layer.shadowRadius = 4;
};

CRBoxInputView *boxInputView = [CRBoxInputView new];
boxInputView.boxFlowLayout.itemSize = CGSizeMake(50, 50);
boxInputView.customCellProperty = cellProperty;
[boxInputView loadAndPrepareViewWithBeginEdit:YES];
```


<br/>

### <a id="Anchor_Line"></a>Line
![Line.png](/ReadmeResources/3Line.png "Line.png")
``` objc
CRBoxInputCellProperty *cellProperty = [CRBoxInputCellProperty new];
cellProperty.showLine = YES; //Required
cellProperty.customLineViewBlock = ^CRLineView * _Nonnull{
    CRLineView *lineView = [CRLineView new];
    lineView.underlineColorNormal = color_master;
    lineView.underlineColorSelected = [color_master colorWithAlphaComponent:0.55];
    [lineView.lineView mas_remakeConstraints:^(MASConstraintMaker *make) {
        make.height.mas_equalTo(4);
        make.left.right.bottom.offset(0);
    }];

    return lineView;
}; //Optional

CRBoxInputView *boxInputView = [CRBoxInputView new];
boxInputView.customCellProperty = cellProperty;
[boxInputView loadAndPrepareViewWithBeginEdit:YES];
```


<br/>

### <a id="Anchor_SecretSymbol"></a>SecretSymbol
![SecretSymbol.png](/ReadmeResources/4SecretSymbol.png "SecretSymbol.png")
``` objc
CRBoxInputCellProperty *cellProperty = [CRBoxInputCellProperty new];
cellProperty.securitySymbol = @"*"; //Optional

CRBoxInputView *boxInputView = [CRBoxInputView new];
boxInputView.ifNeedSecurity = YES; //Required (You can change this property anytime. And the existing texts can be refreshed automatically.)
boxInputView.customCellProperty = cellProperty;
[boxInputView loadAndPrepareViewWithBeginEdit:YES];
```


<br/>

### <a id="Anchor_SecretImage"></a>SecretImage
![SecretImage.png](/ReadmeResources/5SecretImage.png "SecretImage.png")
``` objc
CRBoxInputCellProperty *cellProperty = [CRBoxInputCellProperty new];
cellProperty.securityType = CRBoxSecurityCustomViewType; //Required
cellProperty.customSecurityViewBlock = ^UIView * _Nonnull{
    CRSecrectImageView *secrectImageView = [CRSecrectImageView new];
    secrectImageView.image = [UIImage imageNamed:@"smallLock"];
    secrectImageView.imageWidth = 23;
    secrectImageView.imageHeight = 27;

    return secrectImageView;
}; //Required

CRBoxInputView *boxInputView = [CRBoxInputView new];
boxInputView.ifNeedSecurity = YES; //Required (You can change this property anytime. And the existing texts can be refreshed automatically.)
boxInputView.customCellProperty = cellProperty;
[boxInputView loadAndPrepareViewWithBeginEdit:YES];
```


<br/>

### <a id="Anchor_SecretView"></a>SecretView
![SecretView.png](/ReadmeResources/6SecretView.png "SecretView.png")
``` objc
CRBoxInputCellProperty *cellProperty = [CRBoxInputCellProperty new];
cellProperty.securityType = CRBoxSecurityCustomViewType; //Required
cellProperty.customSecurityViewBlock = ^UIView * _Nonnull{
    UIView *customSecurityView = [UIView new];
    customSecurityView.backgroundColor = [UIColor clearColor];

    // circleView
    static CGFloat circleViewWidth = 20;
    UIView *circleView = [UIView new];
    circleView.backgroundColor = color_master;
    circleView.layer.cornerRadius = 4;
    [customSecurityView addSubview:circleView];
    [circleView mas_makeConstraints:^(MASConstraintMaker *make) {
        make.width.height.mas_equalTo(circleViewWidth);
        make.centerX.offset(0);
        make.centerY.offset(0);
    }];

    return customSecurityView;
}; //Optional

CRBoxInputView *boxInputView = [CRBoxInputView new];
boxInputView.ifNeedSecurity = YES; //Required (You can change this property anytime. And the existing texts can be refreshed automatically.)
boxInputView.customCellProperty = cellProperty;
[boxInputView loadAndPrepareViewWithBeginEdit:YES];
```


<br/>

## Properties And Functions
`CRBoxInputCellProperty` class
``` objc
#pragma mark - UI
/**
borderWidth
default：0.5
*/
@property (assign, nonatomic) CGFloat borderWidth;

/**
cell border color
state：while not selected
default：[UIColor colorWithRed:228/255.0 green:228/255.0 blue:228/255.0 alpha:1]
*/
@property (copy, nonatomic) UIColor *cellBorderColorNormal;

/**
cell border color
state：while selected
default：[UIColor colorWithRed:255/255.0 green:70/255.0 blue:62/255.0 alpha:1]
*/
@property (copy, nonatomic) UIColor *cellBorderColorSelected;

/**
cell border color
state：while not contain text, and not selected
default：same value with 'cellBorderColorFilled'
*/
@property (copy, nonatomic) UIColor *__nullable cellBorderColorFilled;

/**
cell background color
state：while not contain text, and not selected
default：[UIColor whiteColor]
*/
@property (copy, nonatomic) UIColor *cellBgColorNormal;

/**
cell background color
state：while selected
default：[UIColor whiteColor]
*/
@property (copy, nonatomic) UIColor *cellBgColorSelected;

/**
cell background color
state：while contain text, and not selected
default：same value with 'cellBgColorFilled'
*/
@property (copy, nonatomic) UIColor *__nullable cellBgColorFilled;


/**
cellCursorColor
default： [UIColor colorWithRed:255/255.0 green:70/255.0 blue:62/255.0 alpha:1]
*/
@property (copy, nonatomic) UIColor *cellCursorColor;

/**
cellCursorWidth
default： 2
*/
@property (assign, nonatomic) CGFloat cellCursorWidth;

/**
cellCursorHeight
default： 32
*/
@property (assign, nonatomic) CGFloat cellCursorHeight;

/**
cornerRadius
default： 4
*/
@property (assign, nonatomic) CGFloat cornerRadius;
```

`CRBoxFlowLayout` class
``` objc
/** ifNeedEqualGap
* default: YES
*/
@property (assign, nonatomic) BOOL ifNeedEqualGap;

@property (assign, nonatomic) NSInteger itemNum;
```

`CRBoxInputView` class
``` objc
/**
ifNeedCursor
*default: YES
*/
@property (assign, nonatomic) BOOL ifNeedCursor;

/**
codeLength
default: 4
*/
@property (nonatomic, assign) NSInteger codeLength;

/**
ifNeedSecurity
desc: You can change this property anytime. And the existing texts can be refreshed automatically.
default: NO
*/
@property (assign, nonatomic) BOOL ifNeedSecurity;

/**
show security delay time
default: 0.3
*/
@property (assign, nonatomic) CGFloat securityDelay;

/**
keyBoardType
default: UIKeyboardTypeNumberPad
*/
@property (assign, nonatomic) UIKeyboardType keyBoardType;

/**
textContentType
desc: You set this 'nil' or 'UITextContentTypeOneTimeCode' to auto fill verify code.
default: nil
*/
@property (null_unspecified,nonatomic,copy) UITextContentType textContentType NS_AVAILABLE_IOS(10_0);

/**
placeholderText
desc: Will show when specific cell is empty, if placeholder text have value.
default：nil
*/
@property (strong, nonatomic) NSString  * _Nullable placeholderText;

@property (copy, nonatomic) TextDidChangeblock textDidChangeblock;
@property (strong, nonatomic) CRBoxFlowLayout *boxFlowLayout;
@property (strong, nonatomic) CRBoxInputCellProperty *customCellProperty;
@property (strong, nonatomic, readonly) NSString  *textValue;
@property (strong, nonatomic) UIView * _Nullable inputAccessoryView;

- (void)loadAndPrepareView;
- (void)clearAll;

/**
loadAndPrepareView
beginEdit: If need begin edit
default: YES
*/
- (void)loadAndPrepareView;
- (void)loadAndPrepareViewWithBeginEdit:(BOOL)beginEdit;

/**
clearAll
beginEdit: If need begin edit
default: YES
*/
- (void)clearAll;
- (void)clearAllWithBeginEdit:(BOOL)beginEdit;

- (UICollectionView *)mainCollectionView;

// Qiuck set
- (void)quickSetSecuritySymbol:(NSString *)securitySymbol;

// You can inherit and call super
- (void)initDefaultValue;

// You can inherit and rewrite
- (UICollectionViewCell *)customCollectionView:(UICollectionView *)collectionView cellForItemAtIndexPath:(NSIndexPath *)indexPath;

```
`CRBoxInputCell` class
``` objc
// You can inherit and rewrite
- (UIView *)createCustomSecurityView;
```

`CRLineView` class
``` objc
@property (strong, nonatomic) UIView    *lineView;

/**
underlineColor
state：while unselected
default：[UIColor colorWithRed:49/255.0 green:51/255.0 blue:64/255.0 alpha:1]
*/
@property (copy, nonatomic) UIColor *underlineColorNormal;

/**
underlineColor
state：while selected
default：[UIColor colorWithRed:49/255.0 green:51/255.0 blue:64/255.0 alpha:1]
*/
@property (copy, nonatomic) UIColor *underlineColorSelected;
```

## Other Problems

- [pod search unable find a pod（already solved）](https://github.com/CRAnimation/CRBoxInputView/issues/1 "pod search unable find a pod") 
- [pod installation failed， [!] Unable to find a specification for CRBoxInputView（already solved）](https://github.com/CRAnimation/CRBoxInputView/issues/2 "pod installation failed， [!] Unable to find a specification for CRBoxInputView")

## Author

BearRan, 648070256@qq.com

## Feedback
If you have any other problems about this widget, you can tell me by send E-mail or open a issuse.

## License

CRBoxInputView is available under the MIT license. See the LICENSE file for more info.
