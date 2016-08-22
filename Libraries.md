# CocoaPods

For integrating third party libraries to our projects we use [CocoaPods](https://cocoapods.org) (what a surprise!). We use latest versions of cocoapods and also latest versions of libraries. We also tried Carthage but we didn't become friends 😐

If you don't know CocoaPods check [official website](https://guides.cocoapods.org) for some guides and docs, it's pretty simple to use.

### Podfile
Always define exact versions of pods or use at least any version definition!

```ruby
# 👍
pod 'SnapKit', '~> 0.22'
pod 'ReactiveCocoa', '4.2'

# 💩
pod 'SDWebImage'
```

Try to group pods to logical blocks eg. UI, networking, analytics etc. It's not necessary but it makes Podfile more pleasant to read and maintain.
```ruby
# Analytics
pod 'Flurry-iOS-SDK', '~> 7.6'
pod 'GoogleAnalytics', '~> 3.16'

# Requests processing
pod 'SwiftyJSON', '~> 2.3'
pod 'Curry', '~> 2.3'
pod 'Argo', '~> 3.1'
pod 'Ogra', '~> 3.1'
```

## Ackee Pods
We develop and maintain useful libraries in Ackee and most of them are opensource, so they are available here on github and default public cocoapods repo, but we also have some private libraries which we cannot share with the world. For this case we have own private cocapods repo. Search `AckeePods` on our GitLab for details.

## CocoaPods & source control
There's nice pros & cons section about using source control in [documentation](https://guides.cocoapods.org/using/using-cocoapods.html). We chose not commit Pods folder to git. We commit only Podfile and Podfile.lock.

# Our favorite third party libraries
Set of Libraries we use during development
### Networking

### Mapping

For mapping JSON objects we use [Argo](https://github.com/thoughtbot/Argo) with reactive extensions we created. It really simplifies asynchronous mapping.

To make our work even simpler we use Argo in combination with [Curry](https://github.com/thoughtbot/Curry). Examples of usage can be found at [Argo github](https://github.com/thoughtbot/Argo).

### CoreData

Our projects use Swift structs and manipulation with them is realised using [CoreValue](https://github.com/terhechte/CoreValue) with some small improvements we made ourselves. Mapping to those structs is handled by [Argo](https://github.com/thoughtbot/Argo).

To simplify our work with CoreData even more we use [MagicalRecord](https://github.com/magicalpanda/MagicalRecord).

Some of our older projects use `NSManagedObject` subclasses to work with database items. Subclasses are generated using [mogenerator](https://github.com/rentzsch/mogenerator). Mapping of those objects is handled by [MagicalRecord](https://github.com/magicalpanda/MagicalRecord) itself _(prefered)_ - some projects use [Groot](https://github.com/gonzalezreal/Groot), but we consider those options to be almost equal.

### AutoLayout
