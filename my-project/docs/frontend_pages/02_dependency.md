To communicate with FastAPI, REST API requests must happen within Flutter. HTTP shall be utilized to do so. In your code editor, navigate to the `tg_flutter` directory and open the `pubspec.yaml` file. Located about line 29 are our app's dependencies. Add the `http` dependecy to your `yaml` file to make it look like it does below. You may or may not be prompted to update the dependencies.

```yaml
dependencies:
 http: ^0.13.4
 url_launcher: ^6.0.18
 flutter:
   sdk: flutter
```

To update your dependencies use the following command from the `tg_flutter` folder.

```
$ flutter pub get
```