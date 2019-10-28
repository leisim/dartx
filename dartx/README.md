<img src="https://raw.githubusercontent.com/leisim/dartx/master/.github/logo.svg?sanitize=true" width="500px">

[![Dart CI](https://github.com/leisim/dartx/workflows/Dart%20CI/badge.svg)](https://github.com/leisim/dartx/actions) [![Codecov](https://img.shields.io/codecov/c/github/leisim/dartx.svg)](https://codecov.io/gh/leisim/dartx) [![dartx](https://img.shields.io/pub/v/dartx?label=dartx)](https://pub.dev/packages/dartx) [![flutterx](https://img.shields.io/pub/v/flutterx?label=flutterx)](https://pub.dev/packages/flutterx)

*If you miss an extension, please open an issue or pull request*

### Resources:
- [Documentation](https://pub.dev/documentation/dartx/latest/dartx/dartx-library.html)
- [Pub Package](https://pub.dev/packages/dartx)
- [GitHub Repository](https://github.com/leisim/dartx)

On this page you can find some of the extensions. Take a look at the docs to see all of them.

## Getting started 🎉

Add the following to you `pubspec.yaml` and replace `[version]` with the latest version:

```dart
dependencies:
  dartx: ^[version]
```

After you import the library, you can use the extensions.

```dart
import 'package:dartx/dartx.dart';

var slice = [1, 2, 3, 4, 5].slice(1, -2); // [2, 3]
```

## Iterable

### slice()
Returns elements at indices between `start` (inclusive) and `end` (inclusive).
```dart
var list = [0, 1, 2, 3, 4, 5];
var last = list.slice(-1); // [5]
var lastHalf = list.slice(3); // [3, 4, 5]
var allButFirstAndLast = list.slice(1, -2); // [1, 2, 3, 4]
```

### sortedBy() & thenBy()
Sort lists by multiple properties.
```dart
var dogs = [
  Dog(name: "Tom", age: 3),
  Dog(name: "Charlie", age: 7),
  Dog(name: "Bark", age: 1),
  Dog(name: "Cookie", age: 4),
  Dog(name: "Charlie", age: 2),
];

var sorted = dogs
    .sortedBy((dog) => dog.name)
    .thenByDescending((dog) => dog.age);
// Bark, Cookie, Charlie (7), Charlie (2), Tom
```

### distinctBy()
Get distinct elements from a list.
```dart
var list = ['this', 'is', 'a', 'test'];
var distinctByLength = list.distinctBy((it) => it.length); // ['this', 'is', 'a']
```

### flatten()
Get a new lazy `Iterable` of all elements from all collections in a collection.
```dart
var nestedList = [[1, 2, 3], [4, 5, 6]];
var flattened = nestedList.flatten(); // [1, 2, 3, 4, 5, 6]
```

## String

### chars
Get a list of single character strings from a string. Supports emojis.
```dart
var chars = 'family👨‍👨‍👧‍👦'.chars; // ['f', 'a', 'm', 'i', 'l', 'y', '👨‍👨‍👧‍👦']
```

### isBlank()
Returns `true` if this string is empty or consists solely of whitespace characters.
```dart
var notBlank = '   .'.isBlank; // false
var blank = '  '.isBlank; // true
```

### toIntOrNull()
Parses the string as an ineger or returns `null` if it is not a number.
```dart
var number = '12345'.toIntOrNull(); // 12345
var notANumber = '123-45'.toIntOrNull(); // null
```

## Time 
Credits to [joboms](https://github.com/jogboms)!
```dart
final Duration tenMinutes = 10.minutes;
final DateTime afterTenMinutes = DateTime.now() + 10.minutes;
final Duration tenMinutesAndSome = 10.minutes + 15.seconds;
final int tenMinutesInSeconds = 10.minutes.inSeconds;
final DateTime tenMinutesLater = 10.minutes.later;
```

You can perform all basic arithmetic operations on `Duration` as you always have been:

```dart
final Duration interval = 10.minutes + 15.seconds - 3.minutes + 2.hours;
final Duration doubled = interval * 2;
```

You can also use these operations on `DateTime`:

```dart
final DateTime oneHourAfter = DateTime() + 1.hours;
```

`Duration` is easily convertible as it always has been:

```dart
final int twoMinutesInSeconds = 2.minutes.inSeconds;
```

You can also convert `Duration` to `DateTime`, if needed:

```dart
final DateTime timeInFuture = 5.minutes.later;
final DateTime timeInPast = 5.minutes.ago;
```


## Function

### invoke()
Executes a function. This is very useful for `null` checks.
```dart
var func = (String value) {
  print(value);
}

func?.invoke('hello world');
```

### partial(), partial2() ...
Applies some of the required arguments to a function and returns a function which takes the remaining arguments.
```dart
void greet(String firstName, String lastName) {
  print('Hi $firstName $lastName!');
}

var greetStark = greet.partial('Stark');
greetStark('Sansa'); // Hi Sansa Stark!
greetStark('Tony'); // Hi Tony Stark!
```

## File

### name
Get the name and extension of a file.
```dart
var file = File('some/path/testFile.dart');
print(file.name); // testFile.dart
print(file.nameWithoutExtension); // testFile
```

### appendText()
Append text to a file.
```dart
await File('someFile.json').appendText('{test: true}');
```

### isWithin()
Checks if a file is inside a directory.
```dart
var dir = Directory('some/path');
File('some/path/file.dart').isWithin(dir); // true
```


## License
```
Copyright 2019 Simon Leier

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
