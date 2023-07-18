# Flutter_doc_CokBK_Des_Use_a_custom_font
 https://docs.flutter.dev/cookbook/design/fonts
Use a custom font
=================

1.  [Cookbook](https://docs.flutter.dev/cookbook)
2.  [Design](https://docs.flutter.dev/cookbook/design)
3.  [Use a custom font](https://docs.flutter.dev/cookbook/design/fonts)

Although Android and iOS offer high quality system fonts, one of the most common requests from designers is for custom fonts. For example, you might have a custom-built font from a designer, or perhaps you downloaded a font from [Google Fonts](https://fonts.google.com/).

info Note: Check out the [google_fonts](https://pub.dev/packages/google_fonts) package for direct access to over 1,000 open-sourced font families.

info Note: For another approach to using custom fonts, especially if you want to re-use one font over multiple projects, see [Export fonts from a package](https://docs.flutter.dev/cookbook/design/package-fonts).

Flutter works with custom fonts and you can apply a custom font across an entire app or to individual widgets. This recipe creates an app that uses custom fonts with the following steps:

1.  Import the font files.
2.  Declare the font in the pubspec.
3.  Set a font as the default.
4.  Use a font in a specific widget.

[](https://docs.flutter.dev/cookbook/design/fonts#1-import-the-font-files)1\. Import the font files
---------------------------------------------------------------------------------------------------

To work with a font, import the font files into the project. It's common practice to put font files in a `fonts` or `assets` folder at the root of a Flutter project.

For example, to import the Raleway and Roboto Mono font files into a project, the folder structure might look like this:

content_copy

```
awesome_app/
  fonts/
    Raleway-Regular.ttf
    Raleway-Italic.ttf
    RobotoMono-Regular.ttf
    RobotoMono-Bold.ttf

```

### [](https://docs.flutter.dev/cookbook/design/fonts#supported-font-formats)Supported font formats

Flutter supports the following font formats:

-   `.ttc`
-   `.ttf`
-   `.otf`

Flutter does not support `.woff` and `.woff2` fonts for all platforms.

[](https://docs.flutter.dev/cookbook/design/fonts#2-declare-the-font-in-the-pubspec)2\. Declare the font in the pubspec
-----------------------------------------------------------------------------------------------------------------------

Once you've identified a font, tell Flutter where to find it. You can do this by including a font definition in the `pubspec.yaml` file.

content_copy

```
flutter:
  fonts:
    - family: Raleway
      fonts:
        - asset: fonts/Raleway-Regular.ttf
        - asset: fonts/Raleway-Italic.ttf
          style: italic
    - family: RobotoMono
      fonts:
        - asset: fonts/RobotoMono-Regular.ttf
        - asset: fonts/RobotoMono-Bold.ttf
          weight: 700

```

### [](https://docs.flutter.dev/cookbook/design/fonts#pubspecyaml-option-definitions)`pubspec.yaml` option definitions

The `family` determines the name of the font, which you use in the [`fontFamily`](https://api.flutter.dev/flutter/painting/TextStyle/fontFamily.html) property of a [`TextStyle`](https://api.flutter.dev/flutter/painting/TextStyle-class.html) object.

The `asset` is a path to the font file, relative to the `pubspec.yaml` file. These files contain the outlines for the glyphs in the font. When building the app, these files are included in the app's asset bundle.

A single font can reference many different files with different outline weights and styles:

-   The `weight` property specifies the weight of the outlines in the file as an integer multiple of 100, between 100 and 900. These values correspond to the [`FontWeight`](https://api.flutter.dev/flutter/dart-ui/FontWeight-class.html) and can be used in the [`fontWeight`](https://api.flutter.dev/flutter/painting/TextStyle/fontWeight.html) property of a [`TextStyle`](https://api.flutter.dev/flutter/painting/TextStyle-class.html) object. For example, if you want to use the `RobotoMono-Bold` font defined above, you would set `fontWeight` to `FontWeight.w700` in your `TextStyle`.

    Note that defining the `weight` property does not override the actual weight of the font. You would not be able to access `RobotoMono-Bold` with `FontWeight.w100`, even if its `weight` was set to 100.

-   The `style` property specifies whether the outlines in the file are `italic` or `normal`. These values correspond to the [`FontStyle`](https://api.flutter.dev/flutter/dart-ui/FontStyle.html) and can be used in the [`fontStyle`](https://api.flutter.dev/flutter/painting/TextStyle/fontStyle.html) property of a [`TextStyle`](https://api.flutter.dev/flutter/painting/TextStyle-class.html) object. For example, if you want to use the `Raleway-Italic` font defined above, you would set `fontStyle` to `FontStyle.italic` in your `TextStyle`.

    Note that defining the `style` property does not override the actual style of the font; You would not be able to access `Raleway-Italic` with `FontStyle.normal`, even if its `style` was set to normal.

[](https://docs.flutter.dev/cookbook/design/fonts#3-set-a-font-as-the-default)3\. Set a font as the default
-----------------------------------------------------------------------------------------------------------

You have two options for how to apply fonts to text: as the default font or only within specific widgets.

To use a font as the default, set the `fontFamily` property as part of the app's `theme`. The value provided to `fontFamily` must match the `family` name declared in the `pubspec.yaml`.

content_copy

```
return MaterialApp(
  title: 'Custom Fonts',
  // Set Raleway as the default app font.
  theme: ThemeData(fontFamily: 'Raleway'),
  home: const MyHomePage(),
);
```

For more information on themes, see the [Using Themes to share colors and font styles](https://docs.flutter.dev/cookbook/design/themes) recipe.

[](https://docs.flutter.dev/cookbook/design/fonts#4-use-the-font-in-a-specific-widget)4\. Use the font in a specific widget
---------------------------------------------------------------------------------------------------------------------------

If you want to apply the font to a specific widget, such as a `Text` widget, provide a [`TextStyle`](https://api.flutter.dev/flutter/painting/TextStyle-class.html) to the widget.

In this example, apply the RobotoMono font to a single `Text` widget. Once again, the `fontFamily` must match the `family` name declared in the `pubspec.yaml`.

content_copy

```
child: Text(
  'Roboto Mono sample',
  style: TextStyle(fontFamily: 'RobotoMono'),
),
```

### [](https://docs.flutter.dev/cookbook/design/fonts#textstyle)TextStyle

If a [`TextStyle`](https://api.flutter.dev/flutter/painting/TextStyle-class.html) object specifies a weight or style for which there is no exact font file, the engine uses one of the more generic files for the font and attempts to extrapolate outlines for the requested weight and style.

[](https://docs.flutter.dev/cookbook/design/fonts#complete-example)Complete example
-----------------------------------------------------------------------------------

### [](https://docs.flutter.dev/cookbook/design/fonts#fonts)Fonts

The Raleway and RobotoMono fonts were downloaded from [Google Fonts](https://fonts.google.com/).

### [](https://docs.flutter.dev/cookbook/design/fonts#pubspecyaml)`pubspec.yaml`

content_copy

```
name: custom_fonts
description: An example of how to use custom fonts with Flutter

dependencies:
  flutter:
    sdk: flutter

dev_dependencies:
  flutter_test:
    sdk: flutter

flutter:
  fonts:
    - family: Raleway
      fonts:
        - asset: fonts/Raleway-Regular.ttf
        - asset: fonts/Raleway-Italic.ttf
          style: italic
    - family: RobotoMono
      fonts:
        - asset: fonts/RobotoMono-Regular.ttf
        - asset: fonts/RobotoMono-Bold.ttf
          weight: 700
  uses-material-design: true

```

### [](https://docs.flutter.dev/cookbook/design/fonts#maindart)`main.dart`

content_copy

```
import 'package:flutter/material.dart';

void main() => runApp(const MyApp());

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Custom Fonts',
      // Set Raleway as the default app font.
      theme: ThemeData(fontFamily: 'Raleway'),
      home: const MyHomePage(),
    );
  }
}

class MyHomePage extends StatelessWidget {
  const MyHomePage({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      // The AppBar uses the app-default Raleway font.
      appBar: AppBar(title: const Text('Custom Fonts')),
      body: const Center(
        // This Text widget uses the RobotoMono font.
        child: Text(
          'Roboto Mono sample',
          style: TextStyle(fontFamily: 'RobotoMono'),
        ),
      ),
    );
  }
}
```

![Custom Fonts Demo](https://docs.flutter.dev/assets/images/docs/cookbook/fonts.png)
