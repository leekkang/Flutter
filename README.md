# Flutter

* [Document]
* [Blog Reference]
* A Repository that organizes the findings of the Flutter.

* [Dart Document]
* [Dart Linter Rule]

## [Test Drive](https://flutter-ko.dev/docs/get-started/test-drive?tab=vscode)

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

## [Tutorial App](https://codelabs.developers.google.com/codelabs/first-flutter-app-pt2/#0)

* App code of scrolling + favorited icon + child widget

```
import 'package:flutter/material.dart';
import 'package:english_words/english_words.dart';

// like as lambda expression
void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // package of english_words
    final wordPair = WordPair.random();
    return MaterialApp(
      theme: ThemeData(
        primaryColor: Colors.white,
      ),
      home: RandomWords(),
      // Comment out if you have created a bar in RandomWordsState.
      //title: 'Startup Name Generator',
      // home: Scaffold(
      //   appBar: AppBar(
      //     title: Text('Startup Name Generator'),
      //   ),
      //   body: Center(
      //     child: RandomWords(),
      //   ),
      // ),
    );
  }
}

class RandomWordsState extends State<RandomWords> {
  // underscore variable is private identifier in Dart language
  final _suggestions = <WordPair>[];
  final _saved = Set<WordPair>();
  final _biggerFont = const TextStyle(fontSize: 18.0);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Startup Name Generator'),
        actions: [
          IconButton(icon: Icon(Icons.list), onPressed: _pushSaved),
        ],
      ),
      body: _buildSuggestions(),
    );
  }

  Widget _buildRow(WordPair pair) {
    final alreadySaved = _saved.contains(pair);
    return ListTile(
      title: Text(
        pair.asPascalCase,
        style: _biggerFont,
      ),
      trailing: Icon(
        alreadySaved ? Icons.favorite : Icons.favorite_border,
        color: alreadySaved ? Colors.red : null,
      ),
      onTap: () {
        setState(() {
          if (alreadySaved) {
            _saved.remove(pair);
          } else {
            _saved.add(pair);
          }
        });
      },
    );
  }

  Widget _buildSuggestions() {
    return ListView.builder(
        padding: const EdgeInsets.all(16.0),
        // like as anonymous function
        itemBuilder: (context, i) {
          // Designated to show up to 15 items only.
          if (i > 30) return null;

          // For odd rows, the function adds a Divider widget to visually separate the entries.
          if (i.isOdd) return Divider();

          // equal to (a / b).truncate().toInt() if index is [double]
          final index = i ~/ 2;
          if (index >= _suggestions.length) {
            // If you’ve reached the end of the available word pairings,
            // then generate 10 more and add them to the suggestions list.
            _suggestions.addAll(generateWordPairs().take(10));
          }
          return _buildRow(_suggestions[index]);
        });
  }

  // This is a function that moves to the child widget.
  void _pushSaved() {
    Navigator.of(context).push(
      MaterialPageRoute<void>(
        builder: (BuildContext context) {
          final tiles = _saved.map(
            (WordPair pair) {
              return ListTile(
                title: Text(
                  pair.asPascalCase,
                  style: _biggerFont,
                ),
              );
            },
          );
          final divided = ListTile.divideTiles(
            context: context,
            tiles: tiles,
          ).toList();

          return Scaffold(
            appBar: AppBar(
              title: Text('Saved Suggestions'),
            ),
            body: ListView(children: divided),
          );
        },
      ),
    );
  }
}

class RandomWords extends StatefulWidget {
  @override
  RandomWordsState createState() => RandomWordsState();
}

```

[Document]: https://flutter-ko.dev/docs/get-started/install
[Blog Reference]: https://medium.com/@pks2974/flutter-%EA%B0%84%EB%8B%A8-%EC%A0%95%EB%A6%AC%ED%95%98%EA%B8%B0-9532e16aff57
[Dart Document]: https://dart.dev/guides/language/effective-dart
[Dart Linter Rule]: https://dart-lang.github.io/linter/lints/index.html