# Third party libraries

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

