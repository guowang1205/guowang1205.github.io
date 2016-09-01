---
Date: 2016-09-01  
Title: iOS NSAttributedString（属性字符串）  
Published: true  
layout: post  
keywords:blog
tags: [iOS开发]
---
**简介**本人是一个iOS开发菜鸟，之前很是懒惰，以后希望以此来激励自己，每天对掌握的新知识点进行记录，激励自己也想分享一下！不怕错，更不怕批！只为自己好好的学习留下点努力的痕迹！
    
NSAttributedString实际上就是一个字符串和一本字典。字典包含每一个字符的属性：包括字体、大小、下划线、颜色等等。关键是要知道字典中每个key的含义以及相应value的取值范围。 


<font color=#0099ff size=5 face="黑体">Character Attributes（重点）</font>


```
NSString *const  NSFontAttributeName ;                   // 设置字体，UIFont对象，默认12-point Helvetica(Neue)
NSString *const  NSParagraphStyleAttributeName ;         // （重要）设置段落风格，NSParagraphStyle对象，默认是[NSParagraphStyle defaultParagraphStyle]，这里可以设置很多段落格式，首行缩进之类的
NSString *const  NSForegroundColorAttributeName ;        // 字体颜色，UIColor对象，默认黑色
NSString *const  NSBackgroundColorAttributeName ;        // 背景色，UIColor对象，默认透明
NSString *const  NSLigatureAttributeName ;               // <span style="color:#FF0000;">（********）不知道干嘛用</span>
NSString *const  NSKernAttributeName ;                   // 字符间距，NSNumber 浮点数，默认为0
NSString *const  NSStrikethroughStyleAttributeName ;     // 删除线的线粗，NSNumber 整数，默认是NSUnderlineStyleNone（你真的没看错）
NSString *const  NSUnderlineStyleAttributeName ;         // 下划线的线粗，NSNumber 整数，默认同上，还有别的样式，例如双下划线
NSString *const  NSStrokeColorAttributeName ;            // 描边颜色，UIColor对象，默认同字体颜色
NSString *const  NSStrokeWidthAttributeName ;            // 描边，NSNumber 浮点数，正值表示镂空描边，负值标志填充描边，值表示描边线粗
NSString *const  NSShadowAttributeName ;                 // 阴影，NSShadow对象，效果参照最后的图片
NSString *const  NSTextEffectAttributeName ;             // 文本风格，NSSting对象，默认为nil，官方举例NSTextEffectLetterpressStyle，其实也就只有这个风格。。。感觉有跟没有差不多
NSString *const  NSAttachmentAttributeName ;             // <span style="color:#FF0000;">（********）文本附件属性</span>， NSTextAttachment对象，其中包含有图片，等我找到典型案例再回来重新介绍
NSString *const  NSLinkAttributeName ;                   // 链接某个地址，NSURL(推荐)或NSString对象，默认为nil不指定任何链接。这里有详细介绍，http://blog.csdn.net/reylen/article/details/18958995
NSString *const  NSBaselineOffsetAttributeName ;         // 基线偏移量，NSNumber 浮点数，可以上下微调字体的位置。（适合那些返回位置信息不正确的字体）
NSString *const  NSUnderlineColorAttributeName ;         // 下划线颜色
NSString *const  NSStrikethroughColorAttributeName ;     // 删除线颜色
NSString *const  NSObliquenessAttributeName ;            // 斜体，NSNumber 浮点数，默认0，数值表示倾斜度
NSString *const  NSExpansionAttributeName ;              // 水平拉伸，NSNumber 浮点数，默认0，水平拉伸字体，高度不变。
NSString *const  NSWritingDirectionAttributeName ;       // <span style="color:#FF0000;">（********）</span>书写方向，NSArray NSNumber（而且只能是整数0，1，2，3），没看到什么效果，找到案例再来更新
NSString *const  NSVerticalGlyphFormAttributeName;       // 水平或垂直显示，NSNumber（只有0：水平和1：垂直），没看到效果。。。
```

Text Writing Direction

用于"NSWritingDirectionAttributeName"

```
Text Writing Direction

用于"NSWritingDirectionAttributeName"
```

Text Effect Attribute

用于"NSTextEffectAttributeName"

```
Text Effect Attribute

用于"NSTextEffectAttributeName"

```
Underline and Strikethrough Style Attributes

用于"NSUnderlineStyleAttributeName"和"NSStrikethroughStyleAttributeName"

```
typedef enum : NSInteger  {
   NSUnderlineStyleNone  = 0x00 ,
   NSUnderlineStyleSingle  = 0x01 ,
   NSUnderlineStyleThick  = 0x02 ,
   NSUnderlineStyleDouble  = 0x09 ,
   NSUnderlinePatternSolid  = 0x0000 ,
   NSUnderlinePatternDot  = 0x0100 ,
   NSUnderlinePatternDash  = 0x0200 ,
   NSUnderlinePatternDashDot  = 0x0300 ,
   NSUnderlinePatternDashDotDot  = 0x0400 ,
   NSUnderlineByWord  = 0x8000 
} NSUnderlineStyle;
```
String Drawing Options


```
enum {
   NSStringDrawingTruncatesLastVisibleLine  = 1 << 5,
   NSStringDrawingUsesLineFragmentOrigin  = 1 << 0,
   NSStringDrawingUsesFontLeading  = 1 << 1,
   NSStringDrawingUsesDeviceMetrics  = 1 << 3,
};
typedef NSInteger  NSStringDrawingOptions;

```
Document Types

```
NSString  *NSPlainTextDocumentType;
NSString  *NSRTFTextDocumentType;
NSString  *NSRTFDTextDocumentType;
NSString  *NSHTMLTextDocumentType;
```

Keys for Options and Document Attributes Dictionaries

```
NSString *const  NSDocumentTypeDocumentAttribute ;
NSString *const  NSCharacterEncodingDocumentAttribute ;
NSString *const  NSDefaultAttributesDocumentAttribute ;
NSString *const  NSPaperSizeDocumentAttribute ;
NSString *const  NSPaperMarginDocumentAttribute ;
NSString *const  NSViewSizeDocumentAttribute ;
NSString *const  NSViewZoomDocumentAttribute ;
NSString *const  NSViewModeDocumentAttribute ;
NSString *const  NSReadOnlyDocumentAttribute ;
NSString *const  NSBackgroundColorDocumentAttribute ;
NSString *const  NSHyphenationFactorDocumentAttribute ;
NSString *const  NSDefaultTabIntervalDocumentAttribute ;
NSString *const  NSTextLayoutSectionsAttribute;
```
Text Layout Sections Attribute

```
NSString  *NSTextLayoutSectionOrientation;
NSString  *NSTextLayoutSectionRange;
```

**NSString的属性常量，貌似部分可以用在Character Attributes里面
**
UILineBreakMode已由NSLineBreakMode代替。Keys for Text Attributes Dictionaries已在ios 7中被抛弃。剩下以下三类常量可以使用。

NSTextAlignment：

```
enum {  
   NSTextAlignmentLeft       = 0,  
   NSTextAlignmentCenter     = 1,  
   NSTextAlignmentRight      = 2,  
   NSTextAlignmentJustified  = 3,   // 两端对齐  
   NSTextAlignmentNatural    = 4,  
};  
typedef NSInteger  NSTextAlignment;  
```
UIBaselineAdjustment：

用于"NSBaselineOffsetAttributeName"字符属性

```
typedef enum {  
   UIBaselineAdjustmentAlignBaselines ,   // 根据文字的baseLine调整  
   UIBaselineAdjustmentAlignCenters ,     // 根据框的水平中心线调整  
   UIBaselineAdjustmentNone ,             // 以左上角为基准，默认对齐方式  
} UIBaselineAdjustment;  
```

NSWritingDirection：

```
enum {  
   NSWritingDirectionNatural  = -1,      // Use the Unicode Bidi algorithm rules P2 and P3 to determine which direction to use.  
   NSWritingDirectionLeftToRight  =  0,  // 从左到右  
   NSWritingDirectionRightToLeft  =  1   // 从右到左  
};  
```
***
## UITextViewDelegate调用流程：

### 1.点击TextView内部，出现光标前。

```
- (BOOL)textViewShouldBeginEditing:(UITextView *)textView;  
```

如果返回NO，则不会进入编辑，不会出现光标，也不会调用textViewDidBeginEditing:方法。

当选定点选字符串中其他位置，还是会调用didChangeSelection方法
### 2.出现光标后

```
- (void)textViewDidBeginEditing:(UITextView *)textView;  
```
### 3.移动光标或选定某些字符串

```
- (void)textViewDidChangeSelection:(UITextView *)textView;  

```
### 4.添加、删除一个字符

```
- (BOOL)textView:(UITextView *)textView shouldChangeTextInRange:(NSRange)range replacementText:(NSString *)text;  
- (void)textViewDidChangeSelection:(UITextView *)textView;  
```

```
- (void)textViewDidChange:(UITextView *)textView;  
```

如果第1个方法返回NO，不会调用下面两个方法。

### 5.不知道怎么结束编辑。。。先留着。（***）
---

#### 附类定义

## UITextView

```
NS_CLASS_AVAILABLE_IOS(2_0) @interface UITextView : UIScrollView <UITextInput>

@property(nonatomic,assign) id<UITextViewDelegate> delegate;    // 代理
@property(nonatomic,copy) NSString *text;
@property(nonatomic,retain) UIFont *font;
@property(nonatomic,retain) UIColor *textColor;
@property(nonatomic) NSTextAlignment textAlignment;    // default is NSLeftTextAlignment

@property(nonatomic) NSRange selectedRange;
@property(nonatomic,getter=isEditable) BOOL editable;
@property(nonatomic,getter=isSelectable) BOOL selectable NS_AVAILABLE_IOS(7_0); // toggle selectability, which controls the ability of the user to select content and interact with URLs & attachments
@property(nonatomic) UIDataDetectorTypes dataDetectorTypes NS_AVAILABLE_IOS(3_0);

@property(nonatomic) BOOL allowsEditingTextAttributes NS_AVAILABLE_IOS(6_0); // defaults to NO
@property(nonatomic,copy) NSAttributedString *attributedText NS_AVAILABLE_IOS(6_0); // default is nil
@property(nonatomic,copy) NSDictionary *typingAttributes NS_AVAILABLE_IOS(6_0); // automatically resets when the selection changes

- (void)scrollRangeToVisible:(NSRange)range;


// Presented when object becomes first responder.  If set to nil, reverts to following responder chain.  If
// set while first responder, will not take effect until reloadInputViews is called.
@property (readwrite, retain) UIView *inputView;             
@property (readwrite, retain) UIView *inputAccessoryView;

@property(nonatomic) BOOL clearsOnInsertion NS_AVAILABLE_IOS(6_0); // defaults to NO. if YES, the selection UI is hidden, and inserting text will replace the contents of the field. changing the selection will automatically set this to NO.

// Create a new text view with the specified text container (can be nil) - this is the new designated initializer for this class
- (instancetype)initWithFrame:(CGRect)frame textContainer:(NSTextContainer *)textContainer NS_AVAILABLE_IOS(7_0);

// Get the text container for the text view
@property(nonatomic,readonly) NSTextContainer *textContainer NS_AVAILABLE_IOS(7_0);
// Inset the text container's layout area within the text view's content area
@property(nonatomic, assign) UIEdgeInsets textContainerInset NS_AVAILABLE_IOS(7_0);

// Convenience accessors (access through the text container)
@property(nonatomic,readonly) NSLayoutManager *layoutManager NS_AVAILABLE_IOS(7_0);
@property(nonatomic,readonly,retain) NSTextStorage *textStorage NS_AVAILABLE_IOS(7_0);

// Style for links
@property(nonatomic, copy) NSDictionary *linkTextAttributes NS_AVAILABLE_IOS(7_0);

@end

UIKIT_EXTERN NSString * const UITextViewTextDidBeginEditingNotification;
UIKIT_EXTERN NSString * const UITextViewTextDidChangeNotification;
UIKIT_EXTERN NSString * const UITextViewTextDidEndEditingNotification;

```

## NSAttributedString


```
@interface NSAttributedString : NSObject <NSCopying, NSMutableCopying, NSSecureCoding>

@property (readonly, copy) NSString *string;
- (NSDictionary *)attributesAtIndex:(NSUInteger)location effectiveRange:(NSRangePointer)range;

@end

@interface NSAttributedString (NSExtendedAttributedString)

@property (readonly) NSUInteger length;
- (id)attribute:(NSString *)attrName atIndex:(NSUInteger)location effectiveRange:(NSRangePointer)range;
- (NSAttributedString *)attributedSubstringFromRange:(NSRange)range;

- (NSDictionary *)attributesAtIndex:(NSUInteger)location longestEffectiveRange:(NSRangePointer)range inRange:(NSRange)rangeLimit;
- (id)attribute:(NSString *)attrName atIndex:(NSUInteger)location longestEffectiveRange:(NSRangePointer)range inRange:(NSRange)rangeLimit;

- (BOOL)isEqualToAttributedString:(NSAttributedString *)other;

- (instancetype)initWithString:(NSString *)str;
- (instancetype)initWithString:(NSString *)str attributes:(NSDictionary *)attrs;
- (instancetype)initWithAttributedString:(NSAttributedString *)attrStr;

typedef NS_OPTIONS(NSUInteger, NSAttributedStringEnumerationOptions) {
  NSAttributedStringEnumerationReverse = (1UL << 1),
  NSAttributedStringEnumerationLongestEffectiveRangeNotRequired = (1UL << 20)
};

- (void)enumerateAttributesInRange:(NSRange)enumerationRange options:(NSAttributedStringEnumerationOptions)opts usingBlock:(void (^)(NSDictionary *attrs, NSRange range, BOOL *stop))block NS_AVAILABLE(10_6, 4_0);
- (void)enumerateAttribute:(NSString *)attrName inRange:(NSRange)enumerationRange options:(NSAttributedStringEnumerationOptions)opts usingBlock:(void (^)(id value, NSRange range, BOOL *stop))block NS_AVAILABLE(10_6, 4_0);

@end

NS_CLASS_AVAILABLE(10_0, 3_2)
@interface NSMutableAttributedString : NSAttributedString

- (void)replaceCharactersInRange:(NSRange)range withString:(NSString *)str;
- (void)setAttributes:(NSDictionary *)attrs range:(NSRange)range;

@end

@interface NSMutableAttributedString (NSExtendedMutableAttributedString)

@property (readonly, retain) NSMutableString *mutableString;

- (void)addAttribute:(NSString *)name value:(id)value range:(NSRange)range;
- (void)addAttributes:(NSDictionary *)attrs range:(NSRange)range;
- (void)removeAttribute:(NSString *)name range:(NSRange)range;

- (void)replaceCharactersInRange:(NSRange)range withAttributedString:(NSAttributedString *)attrString;
- (void)insertAttributedString:(NSAttributedString *)attrString atIndex:(NSUInteger)loc;
- (void)appendAttributedString:(NSAttributedString *)attrString;
- (void)deleteCharactersInRange:(NSRange)range;
- (void)setAttributedString:(NSAttributedString *)attrString;

- (void)beginEditing;
- (void)endEditing;

@end
```

## 代理协议UITextViewDelegate

```
@protocol UITextViewDelegate <NSObject, UIScrollViewDelegate>

@optional

- (BOOL)textViewShouldBeginEditing:(UITextView *)textView;
- (BOOL)textViewShouldEndEditing:(UITextView *)textView;

- (void)textViewDidBeginEditing:(UITextView *)textView;
- (void)textViewDidEndEditing:(UITextView *)textView;

- (BOOL)textView:(UITextView *)textView shouldChangeTextInRange:(NSRange)range replacementText:(NSString *)text;
- (void)textViewDidChange:(UITextView *)textView;

- (void)textViewDidChangeSelection:(UITextView *)textView;

- (BOOL)textView:(UITextView *)textView shouldInteractWithURL:(NSURL *)URL inRange:(NSRange)characterRange NS_AVAILABLE_IOS(7_0);
- (BOOL)textView:(UITextView *)textView shouldInteractWithTextAttachment:(NSTextAttachment *)textAttachment inRange:(NSRange)characterRange NS_AVAILABLE_IOS(7_0);

@end


```

## NSShadow

```
NS_CLASS_AVAILABLE_IOS(6_0) @interface NSShadow : NSObject <NSCopying, NSCoding>

@property (nonatomic, assign) CGSize shadowOffset;      // 影子与字符串的偏移量
@property (nonatomic, assign) CGFloat shadowBlurRadius; // 影子的模糊程度
@property (nonatomic, retain) id shadowColor;           // 影子的颜色

@end
```
## shadow属性的效果

```
NSShadow *shadow = [[NSShadow alloc]init];  
    shadow.shadowOffset = CGSizeMake(5, 5);     // 影子偏移量  
    shadow.shadowColor = [UIColor blueColor];   // 影子颜色  
    shadow.shadowBlurRadius = 20.0;             // 模糊程度  
      
      
    NSDictionary *dict = @{  
                           NSFontAttributeName:[UIFont fontWithName:@"Marion-Italic" size:50.0],  
                           NSShadowAttributeName:shadow,  
                           NSKernAttributeName:@(2)  
                           };  
    textView.attributedText = [[NSAttributedString alloc]initWithString:@"中文究竟是\nEnglishReally" attributes:dict];  
```

![](http://http://guowang1205.github.io/images/20141112181441731.png)












