It's time to explore the actual flutter code. Navigate to the `lib` folder within the `tg_flutter` folder. Open the `main.dart` file.

**A few important things to note about Flutter**:

* For the initial starter code provided, all the code lives in the `lib/main.dart` file
* The app's UI is created with Dart code
* Almost everything is considered a widget. The app itself is a widget and the app's UI can be described as a widget tree

## So what is a [Widget](https://api.flutter.dev/flutter/widgets/Widget-class.html)?
- According to the Flutter Documentation, 'Widgets are the central class hierarchy in the Flutter framework. A widget is an immutable description of part of a user interface. Widgets can be inflated into elements, which manage the underlying render tree.'
- Stateful Widgets: a widget that stores info that can change, such as user input. Widgets themselves cannot be modified oonce created, so Flutter stores state information in a compantion class, the State class 

*Learn more about the fundamentals of Flutter and the nuances of building a web app with Flutter [here](https://docs.flutter.dev/get-started/codelab-web#step-0-get-the-starter-web-app)*.