Now for the meat and potatoes of the project. We have already added the HTTP dependency to our `pubspec.yml` file, so we should be good to integrate the GET requests! First import HTTP into `product_page.dart` and `user_page.dart` like so:

```dart
import 'package:http/http.dart' as http;
import 'dart:async';
import 'dart:convert';
```

## Building a User Class

Let's begin with getting our User information in `user_page.dart`. We must first create a User class to contain what is returned from our userExists endpoint.

```dart
class User {
 final bool success;
 
 User({
   required this.success,
 });
 
 factory User.fromJson(Map<String, dynamic> json) {
   return User(
     success: json['res'],
   );
 }
}
```

## Function Call

Then, a function must be created to call the userExists endpoint within the `_UserPageState` class. 

```dart
Future<User> _userExists() async {
   final url = 'http://127.0.0.1:8000/userExists?user=$id';
   final response = await http.get(Uri.parse(url));
 
   if (response.statusCode == 200) {
     return User.fromJson(jsonDecode(response.body));
   } else {
     throw Exception('Failed to load user');
   }
 }
```
## Text Controllers

Create some text controllers and variablesto get live changes to the inputs.

```dart
TextEditingController idController = TextEditingController();
String id = "";
String _idString = 'Your user will appear here if it exists! ';
bool isVisible = false;
```

## Update Widgets and their Containers

In the body of our main widget, we will be including three Containers. These are nested in the body as a list of 'children'.

```dart
body: Padding(
           padding: EdgeInsets.all(10),
           child: ListView(children:
```

The first container is for the 'User Search' text above the search box.

```dart
Container(
                 alignment: Alignment.center,
                 padding: const EdgeInsets.all(10),
                 margin: const EdgeInsets.only(top: 50),
                 child: const Text(
                   'User Search',
                   style: TextStyle(
                       color: Colors.orange,
                       fontWeight: FontWeight.w500,
                       fontSize: 30),
                 )),
```

The second container is for the actual search box that contains our text controller for our input. This is where the user of the application will search for a user name in our data to see if it exists.

```dart
Container(
               padding:
                   EdgeInsets.only(top: 10, left: 150, right: 150, bottom: 10),
               child: TextField(
                 controller: idController,
                 decoration: InputDecoration(
                   border: OutlineInputBorder(),
                   labelText: 'User ID',
                 ),
               ),
             ),
```

Now for our final container will add the functionality of a user searching the input and populate with the response from the endpoint call. The below code does the following within the controller: set stat with our user id input text on button press, call our `_userExists` function, set our return string to input text IF the `_userExists` function returns the proper result, or else let the user of the application know that they did not input a user id that exists, update the input boxes.

```dart
Container(
                 height: 50,
                 padding: EdgeInsets.only(
                     top: 0, left: 150, right: 150, bottom: 10),
                 child: RaisedButton(
                   textColor: Colors.white,
                   color: Colors.orange,
                   child: Text('Search'), 
                   onPressed: () {
                     print(idController.text);
                     setState(() {
                       id = idController.text;
                     });
 
                     _userExists().then((result) {
                       if (result.success) {
                         print("SUCCESS");
                         setState(() {
                           _idString = idController.text;
                         });
                       } else {
                         setState(() {
                           isVisible = true;
                           _idString =
                               "The user you searched does not exist! Oops!";
                         });
                       }
                     });
                   },
                 )),
```
## Repeat for Recommender Endpoint

## JSON Resources and Sample Input

JSON parsing in Flutter was the most difficult concept for me to grasp, so below are a few resources that helped me understand it better:

-   [Background Parsing](https://docs.flutter.dev/cookbook/networking/background-parsing)
-   [Dart Flutter Parse JSON String Array to Object List](https://www.bezkoder.com/dart-flutter-parse-json-string-array-to-object-list/)

Now follow the code provided to add the product search and product recommendation for the product page.