# Flutter

* [Document]
* [Blog Reference]
* A Repository that organizes the findings of the Flutter.

* [Dart Document]
* [Dart Linter Rule]

## Test Drive

* App code for 1 text and 1 button

```
import 'package:flutter/material.dart';

// like as lambda expression
void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        // below code set toolbar color.
        primarySwatch: Colors.blue,
        // This makes the visual density adapt to the platform.
        // For desktop platforms, the controls will be smaller and
        // closer together (more dense) than on mobile platforms.
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: MyHomePage(title: 'Flutter Demo Home Page'),
    );
  }
}

class MyHomePage extends StatefulWidget {
  MyHomePage({Key key, this.title}) : super(key: key);
  // This widget is the home page of your application.

  // Fields in a Widget subclass are always marked "final".
  final String title;

  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  int _counter = 0;

  void _incrementCounter() {
    // below code rerun the build method.
    // setState(() {
    //   _counter++;
    // });
    setState(() => _counter++);
  }

  @override
  Widget build(BuildContext context) {
    // This method is rerun every time setState is called.
    
    return Scaffold(
      appBar: AppBar(
        // this take the value from the MyHomePage object that was created by
        // the App.build method, and use it to set our appbar title.
        title: Text(widget.title),
      ),
      body: Center(
        // Center is a layout widget. It takes a single child and positions it
        // in the middle of the parent.
        child: Column(
          // It takes a list of children and arranges them vertically.
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text(
              'You have pushed the button this many times:',
            ),
            Text(
              '$_counter',
              style: Theme.of(context).textTheme.headline4,
            ),
          ],
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: _incrementCounter,
        tooltip: 'Increment',
        child: Icon(Icons.add),
      ),
    );
  }
}

```

## Tutorial App

* App code of infinite scrolling

```

```

[Document]: https://flutter-ko.dev/docs/get-started/install
[Blog Reference]: https://medium.com/@pks2974/flutter-%EA%B0%84%EB%8B%A8-%EC%A0%95%EB%A6%AC%ED%95%98%EA%B8%B0-9532e16aff57
[Dart Document]: https://dart.dev/guides/language/effective-dart
[Dart Linter Rule]: https://dart-lang.github.io/linter/lints/index.html