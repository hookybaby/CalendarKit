![CalendarKit](https://user-images.githubusercontent.com/8013017/86503522-a26def80-bdb7-11ea-9610-01f3da015d33.jpg)
[![License](https://img.shields.io/cocoapods/l/CalendarKit.svg?style=flat)](http://cocoadocs.org/docsets/CalendarKit)
[![Platform](https://img.shields.io/cocoapods/p/CalendarKit.svg?style=flat)](http://cocoadocs.org/docsets/CalendarKit)
[![Version](https://img.shields.io/cocoapods/v/CalendarKit.svg?style=flat)](http://cocoadocs.org/docsets/CalendarKit)
[![SwiftPM compatible](https://img.shields.io/badge/SwiftPM-compatible-orange.svg)](#swift-package-manager) 



# CalendarKit
**CalendarKit** is a Swift calendar UI library for iOS and iPadOS. It looks similar to the Apple Calendar app out-of-the-box, while allowing customization when needed. CalendarKit is composed of multiple modules which can be used together or independently.

## Need Help?
If you have a **programming question** about how to use CalendarKit in your application, ask it on StackOverflow with the [CalendarKit](https://stackoverflow.com/questions/tagged/calendarkit) tag.

Please, use [GitHub Issues](https://github.com/richardtop/CalendarKit/issues) only for reporting a bug or requesting a new feature.


## Examples
[Video](https://streamable.com/zsnu1)

[Try live in a browser](https://appetize.io/app/k85kqpdr1fp79e59f1c4ar8cx4)

To try CalendarKit with CocoaPods issue the following command in the Terminal:
```ruby
pod try CalendarKit
```

## Installation
CalendarKit can be installed with Swift Package Manager or with CocoaPods.
### Swift Package Manager (Xcode 12 or higher)

The preferred way of installing CalendarKit is via the [Swift Package Manager](https://swift.org/package-manager/).

1. In Xcode, open your project and navigate to **File** → **Swift Packages** → **Add Package Dependency...**
2. Paste the repository URL (`https://github.com/richardtop/CalendarKit.git`) and click **Next**.
3. For **Rules**, select **Version (Up to Next Major)** and click **Next**.
4. Click **Finish**.

[Adding Package Dependencies to Your App](https://developer.apple.com/documentation/swift_packages/adding_package_dependencies_to_your_app)

### CocoaPods

To install it, add the following line to your Podfile:

```ruby
pod 'CalendarKit'
```
[Adding Pods to an Xcode project](https://guides.cocoapods.org/using/using-cocoapods.html)

## Usage
1. Subclass `DayViewController`
2. Implement `EventDataSource` protocol to show events.

CalendarKit requires `EventDataSource` to return an array of objects conforming to `EventDescriptor` protocol, specifying all the information needed to display a particular event. You're free to use a default `Event` class as a model or create your own class conforming to the `EventDescriptor` protocol.

```swift
// Return an array of EventDescriptors for particular date
override func eventsForDate(_ date: Date) -> [EventDescriptor] {
  var models = myAppEventStore.getEventsForDate(date) // Get events (models) from the storage / API

  var events = [Event]()

  for model in models {
      // Create new EventView
      let event = Event()
      // Specify StartDate and EndDate
      event.startDate = model.startDate
      event.endDate = model.endDate
      // Add info: event title, subtitle, location to the array of Strings
      var info = [model.title, model.location]
      info.append("\(datePeriod.beginning!.format(with: "HH:mm")) - \(datePeriod.end!.format(with: "HH:mm"))")
      // Set "text" value of event by formatting all the information needed for display
      event.text = info.reduce("", {$0 + $1 + "\n"})
      events.append(event)
  }
  return events
}
```
After receiving an array of events for a particular day, CalendarKit will handle view layout and display.

### Usage
To respond to the user input, override mehtods of `DayViewDelegate`, for example:

```swift
override func dayViewDidSelectEventView(_ eventView: EventView) {
  print("Event has been selected: \(eventview.data)")
}

override func dayViewDidLongPressEventView(_ eventView: EventView) {
  print("Event has been longPressed: \(eventView.data)")
}
```

## Localization
CalendarKit supports localization and uses iOS default locale to display month and day names. First day of the week is also selected according to the iOS locale.

<img src="https://cloud.githubusercontent.com/assets/8013017/22315567/8ba5f9c2-e378-11e6-860d-b94e87a2a45c.PNG" alt="German" width="320"><img src="https://cloud.githubusercontent.com/assets/8013017/22315600/c87e826a-e378-11e6-9280-732982b42077.PNG" alt="Norwegian" width="320">


## Styles
By default, CalendarKit looks similar to the Apple Calendar app and fully supports Dark Mode. If needed, CalendarKit's look can be easily customized. Steps to apply a custom style are as follows:

1. Create a new `CalendarStyle` object (or copy existing one)
2. Change style by updating the properties.
3. Invoke `updateStyle` method with the new `CalendarStyle`.


```Swift
let style = CalendarStyle()
style.backgroundColor = UIColor.black
dayView.updateStyle(style)
```
<img src="https://cloud.githubusercontent.com/assets/8013017/22717896/a2a6c6f2-edae-11e6-8ac3-d9add3d61fb9.png" alt="Light theme" width="320"> <img src="https://user-images.githubusercontent.com/8013017/69188457-3dfe6880-0b25-11ea-9674-39b9f3c1cd00.png" alt="Dark theme" width="320"> 


## Requirements

- iOS 9.0+
- Swift 4+ (Library is written in Swift 5)

## Contributing
The list of features currently in development can be viewed on the [issues](https://github.com/richardtop/CalendarKit/issues) page.

Before contributing, please review [guidelines and code style](https://github.com/richardtop/CalendarKit/blob/master/CONTRIBUTING.md).


## Author

Richard Topchii


## License

**CalendarKit** is available under the MIT license. See the LICENSE file for more info.
