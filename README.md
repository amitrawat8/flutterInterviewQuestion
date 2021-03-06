# Flutter Interview Question

### Difference between Container and row/column

Container

This is the most used widget in every flutter app. It is mostly used to style its child widgets. It takes only one child. Some flutter widgets, focus only on their core functionality and does not contain much styling options. The container widget comes to the rescue and provides you with various common painting, positioning, and sizing widgets.
```dart
Container(
   child: Widget  //Another flutter widget
)
```
Row/Column

These are widgets that can contain multiple child widgets. The row is the widget that can display various child widgets in a horizontal manner. The column displays child widgets in a vertical manner. By default, these widgets don’t support scrolling. It can be enabled by wrapping with other widgets. But, if there are numerous child widgets, it is preferred to use ListView.
```dart
Row(
  children: [
    Container(), // First Widget
    Text(),      // Second Widget
    ----,
    ----,    // Multiple Widgets
  ])
Column(
  children: [
    Container(), // First Widget
    Text(),      // Second Widget
    ----,
    ----,    // Multiple Widgets
  ])

COMPARISON

|-------------------------------|------------------------------------|
|      CONTAINER                |    COLUMN/ROW                      |
|-------------------------------|------------------------------------|
|*Takes exactly one child widget| *Takes multiple (unlimited)        |
|                               |  child widgets.                    |
|                               |                                    |
|*Rich alignment and styling    | *Alignment options available, but  |
| options are available         |  there are no styling options.     | 
|                               |                                    |
|                               |                                    |
|                               |                                    |
|*Flexible width                |*Always takes full available        |
|  (e.g. child width,           |  height (column) /width (row)      |
|     available width, …)       |                                    |
|                               |                                    |
|                               |                                    |
|*Perfect for custom styling    |*Must-use if widgets sit next       |
|    and alignment              | to/above each other                |
|-------------------------------|------------------------------------|
```

### Difference Between Flexible and Expanded 

1. Widget under Flexible are by default WRAP_CONTENT although you can change it using parameter fit.

2. Widget under Expanded is MATCH_PARENT you can change it using flex.


### LifeCycle of StatefulWidget
The lifecycle has the following simplified steps:

    createState()
    mounted == true
    initState()
    didChangeDependencies()
    build()
    didUpdateWidget()
    setState()
    deactivate()
    dispose()
    mounted == false

   1. createState(): When the Framework is instructed to build a StatefulWidget, it immediately calls createState()

   2. mounted is true: When createState creates your state class, a buildContext is assigned to that state. buildContext is, overly simplified, the place in the                               widget tree in which this widget is placed. Here's a longer explanation. All widgets have a bool this.mounted property. It is turned true                              when the buildContext is assigned. It is an error to call setState when a widget is unmounted.

  3.  initState(): This is the first method called when the widget is created (after the class constructor, of course.) initState is called once and only once. It                         must call super.initState().

 4.   didChangeDependencies(): This method is called immediately after initState on the first time the widget is built.

 5.   build(): This method is called often. It is required, and it must return a Widget.

 6.   didUpdateWidget(Widget oldWidget): If the parent widget changes and has to rebuild this widget (because it needs to give it different data), but it's being                                               rebuilt with the same runtimeType, then this method is called. This is because Flutter is re-using the state, which is long                                           lived. In this case, you may want to initialize some data again, as you would in initState.

 7.  setState(): This method is called often from the framework itself and from the developer. Its used to notify the framework that data has changed

 8.   deactivate(): Deactivate is called when State is removed from the tree, but it might be reinserted before the current frame change is finished. This method                         exists basically because State objects can be moved from one point in a tree to another.

 9.   dispose(): dispose() is called when the State object is removed, which is permanent. This method is where you should unsubscribe and cancel all animations,                         streams, etc.

 10.  mounted is false: The state object can never remount, and error will be thrown if setState is called.

```dart
      import 'package:flutter/material.dart';

      class ScreenLifecyle extends StatefulWidget {
      ScreenLifecyleState state;

      //createState(): When the Framework is instructed to build a StatefulWidget, it immediately calls createState()
      @override
      State<StatefulWidget> createState() {
          // TODO: implement createState
          return ScreenLifecyleState();
      }
      }

      class ScreenLifecyleState extends State<ScreenLifecyle> {
      /*
      mounted is true: When createState creates your state class, a buildContext is assigned to that state.
      BuildContext is, overly simplified, the place in the widget tree in which this widget is placed.
      Here's a longer explanation. All widgets have a bool this.mounted property.
      It is turned true when the buildContext is assigned. It is an error to call setState when a widget is unmounted.
      mounted is false: The state object can never remount, and an error is thrown is setState is called.
      */

      /*
      This is the first method called when the widget is created (after the class constructor, of course.)
      initState is called once and only once. It must called super.initState().
      */
      @override
      void initState() {
          // TODO: implement initState
          super.initState();
          print("initState");
      }

      /*
      This method is called immediately after initState on the first time the widget is built.
      */
      @override
      void didChangeDependencies() {
          // TODO: implement didChangeDependencies
          super.didChangeDependencies();
          print("didChangeDependencies");
      }

      /*
      build(): This method is called often. It is required, and it must return a Widget.
      */
      @override
      Widget build(BuildContext context) {
          print("build");

          // TODO: implement build
          return Container();
      }

      /*
      If the parent widget changes and has to rebuild this widget (because it needs to give it different data),
      but it's being rebuilt with the same runtimeType, then this method is called.
      This is because Flutter is re-using the state, which is long lived.
      In this case, you may want to initialize some data again, as you would in initState.
      */
      @override
      void didUpdateWidget(ScreenLifecyle oldWidget) {
          print("didUpdateWidget");

          // TODO: implement didUpdateWidget
          super.didUpdateWidget(oldWidget);
      }

      @override
      void setState(fn) {
          print("setState");

          // TODO: implement setState
          super.setState(fn);
      }

      /*
      Deactivate is called when State is removed from the tree,
      but it might be reinserted before the current frame change is finished.
      This method exists basically because State objects can be moved from one point in a tree to another.
      */
      @override
      void deactivate() {
          // TODO: implement deactivate
          print("deactivate");
          super.deactivate();
      }

      /*
      Dispose is called when the State object is removed, which is permanent.
      This method is where you should unsubscribe and cancel all animations, streams, etc.
      */
      @override
      void dispose() {
          // TODO: implement dispose
          super.dispose();
       }

         @override
          void didChangeAppLifecycleState(AppLifecycleState state) {
              super.didChangeAppLifecycleState(state);
              switch (state) {
              case AppLifecycleState.inactive:
                  print('appLifeCycleState inactive');
                  break;
              case AppLifecycleState.resumed:
                  print('appLifeCycleState resumed');
                  break;
              case AppLifecycleState.paused:
                  print('appLifeCycleState paused');
                  break;
              case AppLifecycleState.suspending:
                  print('appLifeCycleState suspending');
                  break;
              }
          }

    }
```



