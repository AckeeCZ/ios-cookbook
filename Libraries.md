# CocoaPods

For integrating third party libraries to our projects we use combination of [Carthage](https://github.com/Carthage/Carthage) and [Cocoapods](https://cocoapods.org)

If you don't know any of the just check their official websites, they're not complicated to use.

### Cartfile / Podfile

Let's call those files _DependencyFile_ to make things simple 🙂.

Always include any version information about the dependency you use. Mostly we use the `~>` operator with minor version specified. **It's important to always include some version information**

```ruby
# 👍
github 'SnapKit/SnapKit' ~> 4.0
github 'ReactiveCocoa/ReactiveCocoa' ~> 8.0

# 💩
github 'Alamofire/Alamofire'
```

Try to group pods to logical blocks eg. UI, networking, analytics etc. It's not necessary but it makes DependencyFile more pleasant to read and maintain.

```ruby
# Networking
github 'Alamofire/Alamofire' ~> 4.3
github 'Alamofire/AlamofireImage' ~> 4.3

# UI
github 'SnapKit/SnapKit' ~> 4.0
github "danielgindi/Charts" ~> 3.2
```

## Ackee libs
We develop and maintain useful libraries in Ackee and most of them are opensource, so they are available here on GitHub and default public CocoaPods repo, but we also have some private libraries which we cannot share with the world. For this case we have own private CocoaPods repo. Search `AckeePods` on our GitLab for details.

## Dependencies & source control
There's nice pros & cons section about using source control in [documentation](https://guides.cocoapods.org/using/using-cocoapods.html). We chose not commit Pods folder to git. We commit only Podfile + Podfile.lock and Cartfile + Cartfile.lock. Also if using [Carting](https://github.com/artemnovichkov/Carting) we commit the Carthage/xcfilelists directory.

# Our favorite third party libraries
Set of Libraries we use during development

### Database

- [Realm](https://realm.io) - our favorite persistent storage

### Model
- [libPhoneNumber](https://github.com/iziz/libPhoneNumber-iOS) - for validating phone numbers
- [Marshal](https://github.com/utahiosmac/Marshal) - for mapping API reponses to our models

### Networking

- [Alamofire](https://github.com/Alamofire/Alamofire) - base of our networking layer
- [Reqres](https://github.com/AckeeCZ/Reqres) - our library for logging our REQuests and RESponses

### Reactive programming

- [ReactiveSwift](https://github.com/ReactiveCocoa/ReactiveSwift) + [ReactiveCocoa](https://github.com/ReactiveCocoa/ReactiveCocoa) - our favorite framework for reactive programming
- [ACKReactiveExtensions](https://github.com/AckeeCZ/ACKReactiveExtensions) - our set of _ReactiveSwift_ extensions for our mostly used libraries
- [ReactiveLocation](https://github.com/AckeeCZ/ReactiveLocation) - our library for observing location in a reactive way

### UI helpers

- [AlamofireImage](https://github.com/Alamofire/AlamofireImage) - for downloading and caching images
- [AlamofireNetworkActivityIndicator](https://github.com/Alamofire/AlamofireNetworkActivityIndicator) - for handling network activity indicator in status bar
- [Cosmos](https://github.com/evgenyneu/Cosmos) - for star rating
- [Charts](https://github.com/danielgindi/Charts) - for creating graphs
- [RMDateSelectionViewController](https://github.com/CooperRS/RMDateSelectionViewController) - for selecting date selections in action sheet way
- [M13Checkbox](https://github.com/Marxon13/M13Checkbox) - for building checkboxes
- [RMPickerViewController](https://github.com/CooperRS/RMPickerViewController) - for building custom pickers in action sheet way
- [SnapKit](https://github.com/SnapKit/SnapKit) - for autolayout in code
- [TagListView](https://github.com/ElaWorkshop/TagListView) - for displaying various tag views

### Various extensions

- [ACKategories](https://github.com/AckeeCZ/ACKategories) - our set of useful extensions and subclasses