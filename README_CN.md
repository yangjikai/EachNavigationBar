# EachNavigationBar

[![CI Status](http://img.shields.io/travis/Pircate/EachNavigationBar.svg?style=flat)](https://travis-ci.org/Pircate/EachNavigationBar)
[![Version](https://img.shields.io/cocoapods/v/EachNavigationBar.svg?style=flat)](http://cocoapods.org/pods/EachNavigationBar)
[![Carthage compatible](https://img.shields.io/badge/Carthage-compatible-4BC51D.svg?style=flat)](https://github.com/Carthage/Carthage)
[![License](https://img.shields.io/cocoapods/l/EachNavigationBar.svg?style=flat)](http://cocoapods.org/pods/EachNavigationBar)
![iOS 8.0+](https://img.shields.io/badge/iOS-8.0%2B-blue.svg)

## 示例

要运行示例项目，首先克隆 repo 并在 Example 目录运行 `pod install`。

## 版本要求

* iOS 8.0+
* Swift 4

## 安装

EachNavigationBar 可通过 [CocoaPods](http://cocoapods.org) 或者 [Carthage](https://github.com/Carthage/Carthage) 安装, 简单的添加下面一行到你的 Podfile 或者 Cartfile:

### Podfile

```ruby
pod 'EachNavigationBar'
```

### Cartfile
```ruby
github "Pircate/EachNavigationBar"
```

## 预览

![](https://github.com/Pircate/EachNavigationBar/blob/master/demo.gif) 
![](https://github.com/Pircate/EachNavigationBar/blob/master/new_demo.gif)

## 用法

### 导入

Swift
``` swift
import EachNavigationBar
```
Objective-C
``` ObjC
@import EachNavigationBar;
```

### 安装
#### 在设置 window 的 rootViewController 之前调用以下方法（千万别忘了）

Swift
``` swift
UIViewController.setupNavigationBar
```

Objective-C
``` ObjC
[UIViewController swizzle_setupNavigationBar];
```

### 开启

给当前导航栈的 viewControllers 添加一个独立的导航栏。

只对当前导航栈有效，不影响其他导航栈。

Swift
``` swift
let nav = UINavigationController(rootViewController: vc)
nav.navigation.configuration.isEnabled = true
```

Objective-C
``` ObjC
UINavigationController *nav = [[UINavigationController alloc] initWithRootViewController:vc];
nav.global_configuration.isEnabled = YES;
```

###  设置
#### 导航栈全局配置

更多配置请看[这里](https://github.com/Pircate/EachNavigationBar/blob/master/EachNavigationBar/Classes/UINavigationController%2BConfiguration.swift)

Swift
``` swift
let nav = UINavigationController(rootViewController: vc)
nav.navigation.configuration.titleTextAttributes = [.foregroundColor: UIColor.blue]
nav.navigation.configuration.barTintColor = UIColor.red
nav.navigation.configuration.shadowImage = UIImage(named: "shadow")
nav.navigation.configuration.backImage = UIImage(named: "back")
nav.navigation.configuration.setBackgroundImage(UIImage(named: "nav"), for: .any, barMetrics: .default)
```

Objective-C
``` ObjC
UINavigationController *nav = [[UINavigationController alloc] initWithRootViewController:vc];
nav.global_configuration.titleTextAttributes = @{NSForegroundColorAttributeName: UIColor.blueColor};
nav.global_configuration.barTintColor = UIColor.redColor;
nav.global_configuration.shadowImage = [UIImage imageNamed:@"shadow"];
nav.global_configuration.backImage = [UIImage imageNamed:@"back"];
[nav.global_configuration setBackgroundImage:[UIImage imageNamed:@"nav"] for:UIBarPositionAny barMetrics:UIBarMetricsDefault];
```

#### 每个控制器设置
##### 普通设置

Swift
``` swift
// 一般用法同系统组件
navigation.bar  -> EachNavigationBar -> UINavigationBar
navigation.item -> UINavigationItem

// 隐藏导航栏
navigation.bar.isHidden = true

// 设置导航栏透明度
navigation.bar.alpha = 0.5

// 设置标题透明度
navigation.bar.setTitleAlpha(0.5)

// 设置 barButtonItem 透明度
navigation.bar.setTintAlpha(0.5)
// 如果 barButtonItem 是自定义视图
navigation.item.leftBarButtonItem?.customView?.alpha = 0.5
// 如果 barButtonItem 自定义了 tintColor
navigation.item.leftBarButtonItem?.tintColor = navigation.item.leftBarButtonItem?.tintColor?.withAlphaComponent(0.5)

// 移除毛玻璃效果
navigation.bar.isTranslucent = false

// 隐藏底部黑线
navigation.bar.isShadowHidden = true

// 设置状态栏白色文字
navigationController?.navigationBar.barStyle = .black

// 如果想自定义导航栏位置，请将下面属性设为 true
navinavigation.bar.isUnrestoredWhenViewWillLayoutSubviews = true

// 导航栏额外高度
navigation.bar.extraHeight = 14

// 自定义返回按钮事件
navigation.item.leftBarButtonItem?.action = #selector(backBarButtonAction)
```

Objective-C
``` ObjC
self.each_navigationBar.xxx
self.each_navigationItem.xxx
```

##### 大标题设置(iOS 11.0+)

Swift
``` swift
// 显示大标题
if #available(iOS 11.0, *) {
    navigation.bar.prefersLargeTitles = true
}
// 隐藏大标题
if #available(iOS 11.0, *) {
    navigation.bar.prefersLargeTitles = false
}
// 设置大标题透明度
if #available(iOS 11.0, *) {
    navigation.bar.setLargeTitleAlpha(0.5)
}
```

Objective-C
``` ObjC
// 显示大标题
if (@available(iOS 11.0, *)) {
    self.each_navigationBar.prefersLargeTitles = YES;
}
// 隐藏大标题
if (@available(iOS 11.0, *)) {
    self.each_navigationBar.prefersLargeTitles = NO;
}
// 设置大标题透明度
if (@available(iOS 11.0, *)) {
    [self.each_navigationBar setLargeTitleAlpha:0.5];
}
```

#### 调整 UIScrollView 的 contentInset

Swift
``` swift
adjustsScrollViewContentInset(scrollView)
```

Objective-C
``` ObjC
[self adjustsScrollViewContentInset:self.scrollView];
```

#### UITableViewController

请在控制器释放的时候移除观察者

Swift
``` swift
deinit {
    removeObserverForContentOffset()
}
```

Objective-C
``` ObjC
- (void)dealloc {
    [self removeObserverForContentOffset];
}
```

## 作者

Pircate, gao497868860@163.com

## 许可证

EachNavigationBar 可在 MIT 许可证下使用。有关更多信息，请参阅许可证文件。
