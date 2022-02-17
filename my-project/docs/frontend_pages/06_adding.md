Let's begin adding content to our application and start off with something simple, adding a gif to our intro page! Find your favorite gif online, copy the url, and let's display it from the web.

The following line of code is a network call to display images from a url string.

```dart
Image.network('https://example.com/animated-image.gif')
```

Below is the code I included in the body of my `intro_page.dart` to display a TigerGraph inspired gif!
```dart
child: Image.network('https://media2.giphy.com/media/dv7LVj1t6e1wobkYgX/giphy.gif?cid=ecf05e47zs97ng6h05arjp3l73ti4g0wyqr191cgy19bqoa4&rid=giphy.gif&ct=g',
    width: 300,
    height: 400,
    fit: BoxFit.contain,
),
```