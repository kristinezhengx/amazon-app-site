Now that everything has been setup and our images reside in our Cloud Firebase Storage, we are ready to implement code to access our images in our application!

### Configure Main File

First, we must initialize Firebase when our app is run. In `main.dart` file, change your `main()` function to match below.

```dart
Future<void> main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp();
  runApp(MyApp());
}
```
### Implement on Product Page

Next, we move to `product_page.dart` to add the Firebase package to the top of the code.

```dart
import 'package:firebase_storage/firebase_storage.dart';
```

Then, we add a boolean variable to control when image populates under the `_ProductPageState` class variable.

```dart
  bool isButtonPressed = false;
```

Now, a new function is created to get the image from the firebase instance.

```dart
Future _getImage(BuildContext context, String imageName) async {
    String? downloadURL;
    downloadURL =
        await FirebaseStorage.instance.ref().child(imageName).getDownloadURL();

    return downloadURL;
  }
```

Now, inside the Container that handles the `_productExists()` functionalirty, we want to call our new `_getImage()` when our button is pressed.

```dart
                    _productExists().then((result) {
                        // ignore: unnecessary_null_comparison
                        if (result.id != null) {
                          setState(() {
                            _productString = productController.text;
                            _productName = (result.name);
                            _productImgUrl = (result.imgURL);
                            _getImage(
                                context, "test/" + _productString + ".jpeg");
                            print(_productString + ".jpeg");
                            isButtonPressed = true;
                          });
                        } else {
                          setState(() {
                            isVisible = true;
                            _productName = "This product does not exist!";
                          });
                        }
                      }
```

Below that, we want to include the FutureBuilder that Connects to the Image Network to populate our image from the Firebase Storage URL that was created from the user input in the code above.

```dart
if (isButtonPressed)
                FutureBuilder(
                    future:
                        _getImage(context, "test/" + _productString + ".jpeg"),
                    builder: (context, snapshot) {
                      if (snapshot.hasError) {
                        return const Text(
                          "Something went wrong",
                        );
                      }
                      if (snapshot.connectionState == ConnectionState.done) {
                        return Image.network(
                          snapshot.data.toString(),
                        );
                      }
                      return const Center(child: CircularProgressIndicator());
                    })
```

And voila! Firebase should be successfully implemented into our application! Now, when searching products, all of our images will successfully be populated from our Cloud Firebase Storage!