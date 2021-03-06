# persistent_bottom_nav_bar

A persistent bottom navigation bar for Flutter.

![Persistent Behavior](gifs/persistent.gif)

## Styles

`Neumorphic`

![neumorphic1](gifs/neumorphic.gif)

`Style1`

![style1](gifs/style1.gif)

`Style3`

![style3](gifs/style3.gif)

`Style5`

![style5](gifs/style5.gif)

`Style6`

![style6](gifs/style6.gif)

`Style7`

![style7](gifs/style7.gif)

`Style8`

![style8](gifs/style8.gif)

`Neumorphic without subtitle`

![neumorphic2](gifs/neumorphic-nosubs.gif)

Note: These doesn't include all style variations.

## Features

- Highly customizable `persistent` bottom navigation bar.
- Ability to push new screens with or without bottom navigation bar.
- Includes platform specific behavior as an option (specify it in the two navigator functions).
- 12 styles for the bottom navigation bar (includes `BottomNavyBar` and `Neumorphic` style).
- Includes functions for pushing screen with or without the bottom navigation bar i.e. pushNewScreen() and pushNewScreenWithRouteSettings().
- Based on flutter's Cupertino(iOS) bottom navigation bar.
- Can be `translucent` for a particular tab.

## Getting Started

In your flutter project add the dependency:

```yaml
dependencies:
  persistent_bottom_nav_bar: any
```

Persistent bottom navigation bar uses `PersistentTabController` as its controller. Here is how to declare it:

```dart
PersistentTabController _controller;

_controller = PersistentTabController(initialIndex: 0);

```

The main widget then to be declared is `PersistenTabView`. NOTE: This widget includes SCAFFOLD (based on `CupertinoTabScaffold`), so no need to declare it. Following is an example for demonstration purposes:

```dart

class MyApp extends StatelessWidget {
  const MyApp({Key key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return PersistentTabView(
      controller: _controller,
      items: _navBarsItems(),
      screens: _buildScreens(),
      showElevation: true,
      isCurved: false,
      iconSize: 26.0,
      navBarStyle: NavBarStyle.style1, // Choose the nav bar style with this property
      onItemSelected: (index) {
        print(index);
      },
    );
  }
}

```

```dart

    List<Widget> _buildScreens() {
        return [
        HomeScreen(),
        SettingsScreen()
        ];
    }

```

```dart

    List<PersistentBottomNavBarItem> _navBarsItems() {
        return [
        PersistentBottomNavBarItem(
            icon: Icon(CupertinoIcons.home),
            title: ("Home"),
            activeColor: CupertinoColors.activeBlue,
            inactiveColor: CupertinoColors.systemGrey,
        ),
        PersistentBottomNavBarItem(
            icon: Icon(CupertinoIcons.settings),
            title: ("Settings"),
            activeColor: CupertinoColors.activeBlue,
            inactiveColor: CupertinoColors.systemGrey,
        ),
        ];
    }

```

To push a new screen, use the following functions to control the `visibility` of bottom navigation bar on a particular screen. Additionally, `platform specific` behavior can be enabled or disabled from here (`disabled` by default).

If `platform specific` is enabled while pushing a new screen, on `Android` it will push the screen WITHOUT the bottom navigation bar but on `iOS` it will persist the bottom navigation bar. This is the default behavior specified by each platform.

```dart

    pushNewScreen(
        context,
        screen: HomeScreen(),
        platformSpecific: false, // OPTIONAL VALUE. False by default, which means the bottom nav bar will persist
        withNavBar: true, // OPTIONAL VALUE. True by default.
    );

```

```dart

    pushNewScreenWithRouteSettings(
        context,
        settings: RouteSettings(name: HomeScreen.routeName),
        screen: HomeScreen(),
        platformSpecific: false,
        withNavBar: true,
    );

```

If you are pushing a new `modal` screen, use the following function:

```dart

    pushDynamicScreen(
        context,
        screen: HomeModalScreen(),
        platformSpecific: false,
        withNavBar: true,
    );

```

For better understanding, refer to the [example project](https://github.com/BilalShahid13/PersistentBottomNavBar/tree/master/example) in the official git repo.
