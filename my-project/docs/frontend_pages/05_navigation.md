Creating navigation in Flutter is pretty straightforward. In Flutter, screens and pages are called routes. Create two routes, Navigate to the second route using Navigator.push(), and then return to the first route using Navigator.pop() and you will have two pages to display information! The Navigator.push() method adds a route to the stack of routes managed by navigator and the Navigator.pop() method removes the current route from the stack.

In your empty `main.dart` file, paste the following code provided by the [Flutter Navigation docs](https://docs.google.com/document/d/1TB7ZxMQH2AZLN8t5jx1Y8KM7ak7Ra49BCS1bQWazKk4/edit?usp=sharing)

```dart
import 'package:flutter/material.dart';
 
void main() {
 runApp(MyApp());
}
 
class MyApp extends StatelessWidget {
 @override
 Widget build(BuildContext context) {
   return MaterialApp(
     title: 'Amazon App',
     theme: ThemeData(
       primarySwatch: Colors.orange,
       visualDensity: VisualDensity.adaptivePlatformDensity,
     ),
     home: HomePage(),
   );
 }
}
```

Then we want to create a folder within our `lib` directory called `pages`. This folder will hold the `dart` files containing the code for our content pages. Create three new dart files within this folder: `home_page.dart`, `product_page.dart` and `user_page.dart`.

Paste the following code into each file, but change each of the 'HomePage' in the code to match the applicable file name. This is the basic skeleton and structure of each Flutter page.

```dart
import 'package:flutter/material.dart';
 
class ProductPage extends StatefulWidget {
 ProductPage({Key? key}) : super(key: key);
 
 @override
 _ProductPageState createState() => _ProductPageState();
}
 
class _ProductPageState extends State<ProductPage> {
 @override
 Widget build(BuildContext context) {
   return Scaffold();
 }
}
```

We also want to create the controllers and a 'on clicked' function called `_onItemTapped` to control clicking on our Nav Bar. 

```dart
PageController _pageController = PageController();
 List<Widget> _screen = [IntroPage(), UserPage(), ProductPage()];
 int _selectedIndex = 0;
 
 void _onPageChanged(int index) {
   setState(() {
     _selectedIndex = index;
   });
 }
 
 void _onItemTapped(int selectedIndex) {
   _pageController.jumpToPage(selectedIndex);
 }
```

And then initialize!

```dart
return Scaffold(
     body: PageView(
       controller: _pageController,
       children: _screen,
       onPageChanged: _onPageChanged,
       physics: NeverScrollableScrollPhysics(),
     ),
```

Once you've made the appropriate changes to your code, save `main.dart, open a terminal to the `tg_flutter` folder and run `flutter run -d chrome`. A Chrome browser will automatically open and run assuming there are no errors. Here you will find the web application with the navigation bar. 

<center>
![Navigation](/assets/frontend/multiPage.gif)
</center>

[Here](https://www.youtube.com/watch?v=YJEMMhA9udQ) is the tutorial I watched to learn about the implementation of a Navbar in Flutter. The tutorial also gives more information about page persistence. I will not explain the exact implementation, but the please watch the tutorial as it is very helpful! And reference the code provided in the repo.

*Side Note: After you make changes to your `main.dart` file, if you hit `r` in the terminal that the terminal the flutter app is running from, it will hot restart the changes you made while the app is still running! The browser will just reload and your changes should appear as long as there are no errors.*