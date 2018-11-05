# Best practices

## Xcode

### Version

The only recommended version of Apple tools like Xcode is the latest available in the [App Store](https://itunes.apple.com/us/app/xcode/id497799835).

### Project architecture 

We use MVVM for our projects so we encourage to use this pattern everywhere unless you find it really heavy clumsy for your case (i.e some table/collection cell)

### Warnings

I would love to say that we really care about warnings. But I have to be honest warnings ain’t errors. We are trying to avoid them but we don’t make such a fuss about them if there are not tons of them.  

## Version Control

We use [Git](https://git-scm.com) and [GitLab](https://about.gitlab.com). We follow [feature branch workflow](https://confluence.atlassian.com/bitbucket/workflow-for-git-feature-branching-814201830.html) for development with merge requests. We have `master` branch where lays production code. In `development` branch we keep *current* development version of the app. 

### Branching 
For every fix or feature you have to create separate branch. When you are done you create merge request.

### Naming
Name branches with meaningful names which describes what you are trying to do there. When more developers are on the project prefix the name with your initials e.g. `dv/fix-login-action`.

### Merge Requests 
On every project we do merge requests. If there are 2 developers on project they do cross merge requests. If there is less or more developers you can do round robin assignment within a team. Everyone creates MR even senior developer can assign MR to junior on his project. <!--Why? [Here is the explanation]() -->

- Always choose destination branch the one from which you originally branched‼️
- Only `development` branch could be merged into `master` 💀 

### Code review
Code review is done in [GitLab](https://about.gitlab.com). There are 4 levels of reviewer's anger:

| emoji | shortcut          | meaning                                                                                      | merged |   |
|--------|-------------------|----------------------------------------------------------------------------------------------|--------|---|
| ❔      | `:grey_question:`   | I'm probably just bored and want to talk :)                                                 | YES    |   |
| ❕      | `:grey_exclamation:` | I will merge this but you should either not do this again or defend it here in the comments. | YES    |   |
| ❗      | `:exclamation:`     | Won't be merged, unless it's a question and you reply that there's no problem.              | MAYBE     |   |
| 💩      | `:shit:`            | Won't be merged. Also, you should walk through sewers for a month. _(Rarely Used)_           | NO     |   |


Other emojis like ➕ are also used, but we don't need a convention for every emoji out there. ❤ 


## Deployment

### Semantic Versioning

We support [semantic versioning](http://semver.org), and it's important that minor releases are backwards compatible otherwise don't feel shy to make it a major release.

### Instructions 

To see all steps needed for deployment of new version to production see [Releases](Release.md) notes

## Comments

Good code should be self explanatory and comments should not be needed. There are few exceptions like public API and particular piece of code which might not be easily readable for everyone (i.e. functional code).

When they are needed, comments should be used to explain **why** a particular piece of code does something. 

Don't use comments in place of `assertionFailure`s.

It is definitely not allowed to use comments for hiding “unwanted” code in source control. 

Block comments should generally be avoided, as code should be as self-documenting as possible, with only the need for intermittent, few-line explanations. This does not apply to those comments used to generate documentation. Also when commenting methods or classes/structs/etc. don't be lazy to add one more slash so the appledoc can be generated.

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
Use `// TODO:` mark when you want mention piece of code as unfinished or needed for refactoring.

### MARK
Use `// MARK:` for good code structure within a file. Also don't hesitate to use hyphen in section name so Xcode can generate section sepators in method overview.

```swift
// MARK: - Lifecycle methods

override public func viewWillAppear(_ animated: Bool) {
    super.viewWillAppear(animated)

    // Here goes the code
}
```

## Streams, Blocks, delegates

### Streams/Signals

As mentioned in [Ingredients](Ingredients.md) we love [ReactiveSwift](https://github.com/ReactiveCocoa/ReactiveSwift) and we encourage to use `Signal`s everywhere! There are lot of ready-made reactive wrappers for most of Cocoa API (some of them in our repos). Or you can write your own.

### Block
- Asynchronous (e.g. networking operations)
- User inputs with multiple options (e.g. `UIAlertView`'s YES and NO)
- Data source driven inputs (e.g. a table items with action blocks that were defined in the data source)
- Returns many values (for example looking for a field in a collection and returning the field and the `IndexPath`)
- If there’s no tracked state or if state is defined in the same method

### Delegate
- Synchronous (e.g. buttons actions in views that should perform on their parents)
- Shouldn't return values
- Provides control over performing an action (e.g. `UITextField`'s `shouldEndEditing`)
- User input with one action (e.g. buttons actions in views that should perform on their parents)
- If tracked state is shared (if state is stored in a property or a constant)

## View controllers

You should always subclass from `BaseViewController` which has shared logic for the whole project. 

## Views

When layouting views always follow those guidelines ‼️
- Favor using `UIStackView` over layouting views yourself
	- When layouting views use `AutoLayout` we prefer [SnapKit](https://github.com/SnapKit/SnapKit) (see [Tooling](Tooling.md) for more reference)
	- When layouting _collections_ or _repeating views_ use `UICollectionView` or `UITableView`

### Presenting and dismissing View Controllers

- When presenting and dismissing a view controller, no view controller should explicitly present or dismiss, such things should be handled by `FlowCoordinator`.

## Theme

To apply app theme for shared elements we use `theme` namespace on UI elements. So when applying a style to an element, setting font to a label, you should use it. It is not that hard 😎

```swift
label.textColor = UIColor.theme.gray

let button = UIButton.theme.createText()
```

Also adding new styles is as easy as an extension:

```swift
extension Theme where Base: UILabel {
    func makeTitle() -> Theme<Base> {
        base.textColor = UIColor.theme.gray
        base.font = UIFont.theme.regular(14)
        return self
    }
}
```

### Images

Of course we store all images in the asset catalog. We prefer to use vector images so we don't actually have to deal with having multiple images for different scales of devices. So all our images are in PDF format. It is important to make sure that the _preserve vector data checkbox_ is always checked. Then as the images are in vectors we should use just a single scale image. Also we don't like the default rendering mode so we prefer to have this property set so it is clear how the image would render.

![Asset catalog settings][asset_catalog]

Not for every case are vectors a good choice. Sometimes we experienced issues when having a complicated vector image as background of a screen caused some problems (like slow push/pop animation). In this cases are raster images good choice 🙂

### Fonts 
Fonts should be stored in Resource folder. To obtain real name of the Font in the system you can use this method.

```swift
extension UIFont {	
    
    class func printAllFonts() {
        UIFont.familyNames().forEach { family in
            UIFont.fontNamesForFamilyName(family).forEach { font in
                print(font)
            }
        }
    }
}
```

When accessing fonts you should use the `theme` namespace.

### Colors

We store colors in code by keeping there hex codes. They are all in the `theme` namespace so when using them you can find them quickly.


[asset_catalog]:    assets/asset_catalog.png "Asset catalog settings"