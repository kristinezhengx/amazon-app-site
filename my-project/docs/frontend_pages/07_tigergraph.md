Now for the meat and potatoes of the project. We have already added the HTTP dependency to our `pubspec.yml` file, so we should be good to integrate the GET requests! First import HTTP into `product_page.dart` and `user_page.dart` like so:

```dart
import 'package:http/http.dart' as http;
import 'dart:async';
import 'dart:convert';
```

## Building a User Class
Let's begin with getting our User information continuing in `user_page.dart`.

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

## Text Controllers

## Update Widgets and their Containers

## Repeat for Recommender Endpoint

## JSON Resources and Sample Input



Now follow the code provided to add the product search and product recommendation for the product page.