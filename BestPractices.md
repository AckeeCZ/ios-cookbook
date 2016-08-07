# Best practices

## Table of Contents



## Xcode

### Version

The only recommended version of Apple tools like XCode is the lastest available in the [App Store][1].

### Project structure

We have recommended [project structure]() however sometimes you will need to change it or not following it for some reason. Thats fine if you can say thats really necessary. Try to keep it consistent. 

### Project architecture 

We use MVVM for our projects so we encourage to use this pattern everywhere unless you find it really heavy clumsy for your case (i.e some table/collection cell)

### Warnings

I would love to say that we really care about warnings. But I have to be honest warnings ain’t errors. We are trying to avoid them but we don’t make such a fuss about them if there are not tons of them.  

### Plugin compatibility

After upgrading to a new Xcode version plugins will become disabled until their list of compatible Xcode versions gets updated. In case you can't wait for an official update by the plugins' authors you can try to run [this script][3]. Be sure to find out your Xcode's version UUID first and update it in the script.

You can get your Xcode version UUID by running

```shell
/usr/libexec/PlistBuddy -c 'Print DVTPlugInCompatibilityUUID' "$(xcode-select -p)/../Info.plist"
```


## Version Control

We use git and gitlab. we follow [feature branch workflow][4] for development with merge requests. We have `master` branch where lays production code. in `development` branch we keep *current* development version of the app. 

### Branching 
For every fix or feature you have to create separate branch. When you are done. You create merge request.

### Naming
Name branches with meaningful names which describes what you are trying to do there. When more developers are on the project prefix the name with your initials i.e `dv/fix-login-action`

### Merge Requests 
On every project we do merge requests. If there are 2 developers on project they do cross merge requests. If there is less or more developers you can do round robin assignment within a team. Everyone creates MR even senior developer can assign MR to junior on his project. Why? [here is the explanation]()

- Always choose destination branch the one from which you originally branched.‼️
- Only `development`branch could be merged into `master` 💀 

### Code review
Codereview is done in gitlab. There are 4 levels of reviewer's anger:

| emoji | shortcut          | meaning                                                                                      | merged |   |
|--------|-------------------|----------------------------------------------------------------------------------------------|--------|---|
| ❔      | :grey_question:   | I'm probably just bored and want to talk :)                                                 | YES    |   |
| ❕      | :grey_exclamation | I will merge this but you should either not do this again or defend it here in the comments. | YES    |   |
| ❗      | :exclamation:     | Won't be merged, unless it's a question and you reply that there's no problem.              | MAYBE     |   |
| 💩      | :shit:            | Won't be merged. Also, you should walk through sewers for a month. _(Rarely Used)_           | NO     |   |


Other emojis like ➕ are also used, but we dont need a convention for every emoji out there. ❤ 


## Deployment

### Semantic Versioning

We support [semantic versioning][6], and it's important that minor releases are backwards compatible otherwise don't feel shy to make it a major release.

### Instructions 

To see all steps needed for deployment of new version to production see [Releases]()notes

## Comments

Good code should be self explanatory and comments should not be needed. 
There are few exceptions like public API and particular piece of code which might not be easily readable for everyone (i.e. functional code)

When they are needed, comments should be used to explain **why** a particular piece of code does something. 

It is definitely not allowed to use comments for hiding “unwanted” code in source control. 

Block comments should generally be avoided, as code should be as self-documenting as possible, with only the need for intermittent, few-line explanations. This does not apply to those comments used to generate documentation.

**Comments style**

One-line:
```swift
// YOLO: This shouldn’t crash
```

Multiple-lines:

```swift
/*
   QUOTE: It is a truth universally acknowledged, that a single man in possession of a good fortune must be in want of a wife.
However little known the feelings or views of such a man may be on his first entering a neighbourhood, this truth is so well fixed in the minds of the surrounding families, that he is considered as the rightful property of some one or other of their daughters.
 */
```

## Marks

### TODO 
Use // TODO: mark when you want mention piece of code as unfinished or needed for refactoring
### MARK
Use //MARK: for good code structure wthin a file

```swift
// MARK: Lifecycle methods
- (void) viewWillAppear(animated : Bool) {
  …
}
```

## Streams, Blocks, delegates

### Streams/Signals

As mentioned in [Ingredients]() we love ReactiveCocoa and we encourage to use Signals everywhere! There are lot of ready-made reactive wrappers for most of Cocoa API (some of them in our repos). Or you can write your own

### Block
- Asynchronous (For example: networking operations)
- User inputs with multiple options (For example: UIAlertView's YES and NO)
- Data source driven inputs (For example: A table items with action blocks that were defined in the data source)
- Returns many values (For example looking for a field in a collection and returning the field and the indexPath)
- If there’s no tracked state or if state it’s defined in the same method

### Delegate
- Synchronous (For example: buttons actions in views that should perform on their parents)
- Shouldn't return values
- Provides control over performing an action (For example: UITextField's shouldEndEditing)
- User input with one action (For example: buttons actions in views that should perform on their parents)
- If tracked state is shared (if state is stored in a property or a constant)


## View controllers

You should always subclass from `BaseViewController` which has shared logic for whole project. 

## Views

When layouting views always follow those guidelines ‼️
- Favor using `UIStackView`over layouting views yourself whenever possible
	- When layouting views use `Autolayout` we prefer [SnapKit]() see [Tooling]() for more reference
	- When layouting _collections_ or _repeating views_ use `UICollectionView` or `UITableView`


### Naming

Since we use `MVVM` pattern it is recommended that every controller containing data or logic needs to have its ViewModel. 

When naming subclasses of `UIViewController` or friends `UIPageViewController`, `UICollectionViewController`, `UITableViewController`, you don't have to use the `ViewController` suffix.

For example instead of `HYPRecipesTableViewController` you would do `HYPRecipesController`, this applies for both Objective-C and Swift.

### Presenting and dismissing View Controllers

- It's better practice to call `dismissViewControllerAnimated:completion:` in the `UIViewController` that did the presenting, not in the `UIViewController` that was presented.

## Assets

### Images

When design is in Sketch use it’s StyleKit for creating resolution-independent vector images. Rest of the images should be in XCAssets and generated and used with Enums generated via [SwiftGen]()


### Fonts 
Fotns should be stored in Resource folder. To obtain `real` name of the Font in the system use this method 

```swift
extension UIFont {	
  class func printAllFonts() {
    UIFont.familyNames().forEach { (family) in
	  UIFont.fontNamesForFamilyName(family).forEach({ (font) in
	    print(font)
	  })
    }
  }
}
```