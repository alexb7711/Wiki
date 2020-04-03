# Flutter vs. React Native Notes

## Flutter

### About Flutter
* Flutter is Google's SDK for creating apps for IOS, Android, and the web. 
* Uses dart (which is also free and open source).
    * Similar to Java or JavaScript.
    * Object oriented language.
* Allows hot reloading.
* Has Material Design (Google flavor) or Cupertino (iOS-flavor) built in.
* Works with existing code?
* Free and open source.
* Uses a modern react-style framework
    * What is react?
        * A JavaScript library for building user interfaces made by Facebook.
* Flutter uses "layered architecture".
    * They use the term *aggressive composability* which means that widgets just compose other widgets, where widgets are just something (such as padding).
* Core principles 
    * Everything is a widget
        * Widgets are the basic building blocks of all Flutter apps.
    * Composition composition composition
        * Dumb widgets are composed of other dumb widgets to create powerful effects. Think `Container()`.
* User interaction is handled using stateful widgets (rather than stateless widgets).
* More "full" package
    * UI Rendering
    * Unit testing
    * Manage states
    * Widgets are created

### Trying it out
(Website)[https://flutter.dev/docs/codelabs/layout-basics]

From the alignment example, the formatting style is as follows:

```dart
import 'package:flutter_web/material.dart';
import 'package:flutter_web_test/flutter_web_test.dart';
import 'package:flutter_web_ui/ui.dart' as ui;

class MyWidget extends StatelessWidget {          // Extend Stateless/Statefull Widget
  @override                                       // Always override
  Widget build(BuildContext context) {            // Required to define the class
    return Row(                                   // Widget
      mainAxisAlignment: MainAxisAlignment.start, // Widget properties
      children: [                                 // Children that live in side the property
        BlueBox(),                                // Etc...
        BlueBox(),
        BlueBox(),
      ],
    );
  }
}

class BlueBox extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      width: 50,
      height: 50,
      decoration: BoxDecoration(
        color: Colors.blue,
        border: Border.all(),
      ),
    );
  }
}
```
## Comments about flutter
* Default formatting is effective, but messy.
* Odd for someone coming from Python, C/C++, C#. 
* However it is intuitive and the documentation is pretty extensive and easy to understand.

## React Native

### About React Native
* Written in JavaScript
* Hot reloading 
* Rendered with native code 
* React-like, but it uses native components instead of web components as building blocks.
* It has a very XML-like feel.
    * This is JSX - a syntax for embedding XML within JavaScript.
* Give you UI rendering using HTML, CSS, and JavaScript

### Trying it Out
(Website)[https://facebook.github.io/react-native/docs/tutorial]    

From the style example, the formatting style is as follows:

```JavaScript
import React, { Component } from 'react';
import { StyleSheet, Text, View } from 'react-native';

const styles = StyleSheet.create({
  bigBlue: {
    color: 'blue',
    fontWeight: 'bold',
    fontSize: 30,
  },
  red: {
    color: 'red',
  },
});

export default class LotsOfStyles extends Component {                         // App Extends component
  render() {                                                                  // All the stuff you want to draw
    return (
      <View>                                                                  // XML-like styling
        <Text style={styles.red}>just red</Text>
        <Text style={styles.bigBlue}>just bigBlue</Text>
        <Text style={[styles.bigBlue, styles.red]}>bigBlue, then red</Text>
        <Text style={[styles.red, styles.bigBlue]}>red, then bigBlue</Text>
      </View>
    );
  }
}      
```

### Comments about React Native
* A more mature framework
* Similar in coding style (Nesting)
* A more familiar looking structure (coming from ROS and working a little with XML).
* Very similar in API styling as Flutter

## Choice: Flutter
* Developed by Google
* Overall comments by people is that it is more stable
* More Full-featured 
* C-Styled (Dart).

## Moving forward
* Going to try to develop an app 
    * If interested, going to be posting about that soon.
