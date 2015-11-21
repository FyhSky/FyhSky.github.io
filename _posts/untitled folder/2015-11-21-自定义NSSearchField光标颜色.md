---
layout: post
title: "自定义NSSearchField光标颜色"
date: 2015-11-21 15:35:00
comments: true
--- 
自定义NSSearchField光标颜色
============
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;本文主要介绍如何自定义输入框中光标的颜色。如果想自定义NSSearchField样式，请参考老谭的一片文章：[http://www.tanhao.me/pieces/1580.html/](http://www.tanhao.me/pieces/1580.html/)，该文章里面做了一些详细的介绍。

&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;改变光标颜色有两种方法：

&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; 1. 子类化NSSearchFieldCell，重写setUpFieldEditorAttributes方法，代码片段如下。

```
- (NSText *)setUpFieldEditorAttributes:(NSText *)textObj
{
    NSText *text = [super setUpFieldEditorAttributes:textObj];
    [text setBackgroundColor:self.backgroundColor];
    text.drawsBackground = YES;
    [(NSTextView*)text setInsertionPointColor:[NSColor whiteColor]];
    return text;
}

```

&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;NSSearchField获取焦点，要显示光标的时候，都会调用该方法。


&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; 2. 遍历NSSearchField的子视图（subviews）, 取出_NSKeyboardFocusClipView类的对象，然后再取出里面的
NSTextView对象，调用setInsertionPointColor函数，传入想要的颜色，代码片段如下。

```
    if (self.searchField.subviews.count) {
        __block NSView *keyboardFocusClipView;
        [self.searchField.subviews enumerateObjectsUsingBlock:
        						^(id  obj, NSUInteger idx,
												 BOOL *stop) {
            //   NSClassFromString(@"_NSKeyboardFocusClipView");
            if ([obj isKindOfClass:[NSClipView class]]) {
                keyboardFocusClipView = obj;
                *stop = YES;
            }
        }];
        
        if (keyboardFocusClipView) {
            NSView *view = keyboardFocusClipView.subviews[0];
            [(NSTextView*)view setInsertionPointColor:cursorColor];
        }

    }
```



&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;两种方法的不同之处在于：方法一调用的前提，是输入框由无光标到有光标时才触发，如果在有光标的时候想改变光标的颜色，就只能使用方法二；方法二只有在输入框有光标的时候才会起作用，无光标的时候就没法触发。

&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;所以两种方法配合使用，就可以完美实现不同Theme下光标颜色的切换。




