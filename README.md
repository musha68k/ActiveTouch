# ActiveTouch

ActiveTouch is an implementation of ActiveRecord using [TouchDB-iOS](https://github.com/couchbaselabs/TouchDB-iOS) (an implementation of CouchDB for iOS)

* Why not CoreData? 
	Just because it's a complex tool (TouchDB is easier than CoreData).
	
##Contact:

Developed by [Lucas Medeiros](https://www.twitter.com/aspmedeiros)

## Development requirements

* Cocoapods - https://github.com/CocoaPods/CocoaPods

## Install cocoapods

To install cocoapods you will need ruby.

	gem install cocoapods
	
More information about cocoapods:

* https://github.com/CocoaPods/CocoaPods
* http://nsscreencast.com/episodes/5-cocoapods

## Cocoapods

Add the dependency to your `Podfile`:

```ruby

platform :ios

...

pod 'ActiveTouch'

...

```

Run `pod install` to install the dependencies.

## Usage

* First you need to setup the database in you AppDelegate:

```objective-c

#import "ATDatabaseContainer.h"

@implementation ATAppDelegate

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
    [[ATDatabaseContainer sharedInstance] openDatabaseWithName:@"your_database_name"];
    return YES;
}

```

* Create a class that inherits from ATModel

```objective-c

#import <Foundation/Foundation.h>
#import "ATModel.h"

@interface Car : ATModel

@property (nonatomic, copy) NSString *model;
@property (nonatomic, copy) NSString *year;

@end

```

* Getting all cars:

```objective-c

[Car allWithSuccessBlock:^(NSArray *collection) {
    self.cars = [NSMutableArray arrayWithArray:collection];
    [self.tableView reloadData];
} withErrorBlock:^(NSError *error) {
    NSLog(@"Error: %@", error);
}];

```

* Getting all cars using pagination:

```objective-c

[Car allWithLimit:10 skipping:5 withSuccessBlock:^(NSArray *collection) {
        
} withErrorBlock:^(NSError *error) {
        
}];

```

* Finding by _id

```objective-c

Car *car = [Car findById:@"12312-ASADSD"];

```

* Validating model:

	ATModel has a method called isValid that returns a BOOL, by default it returns YES.
	If you want some sort of validation you can override it and validates the model as you wish.

* Creating a car:

```objective-c

Car *car = [[Car alloc] init];
car.model = @"aModel";
car.year = @"aYear";

[car createWithSuccessBlock:^{

} withErrorBlock:^(NSError *error) {
   
}];

```

* Updating a car:

```objective-c

[car updateWithSuccessBlock:^{

} withErrorBlock:^(NSError *error) {
   
}];

```

* Destroying a car:

```objective-c

[car destroyWithSuccessBlock:^{

} withErrorBlock:^(NSError *error) {
   
}];

```

## Requirements

`ActiveTouch` requires iOS 5.x or greater.

## Thanx to

[Eduardo Gurgel](https://github.com/edgurgel) for giving me the project name.

## License

Usage is provided under the [MIT License](http://http://opensource.org/licenses/mit-license.php).  See LICENSE for the full details.

