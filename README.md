# QR Bar Code Scanner Dialog
Plugin to show a simple scanner dialog and capture Bar/QR code easily. Works with Android, iOS and Web. It uses [`html5-qrcode`](https://github.com/mebjas/html5-qrcode) js library for web and [`qr_code_scanner`](https://pub.dev/packages/qr_code_scanner) for Android and iOS

#### Note:
At present, this is the only **flutter web** plugin that support **barcode** scanning


## Get Scanned QR/Bar Code

When a QR code is recognized, the text identified will be set in 'result' of type `Barcode`, which contains the output text as property 'code' of type `String` and scanned code type as property 'format' which is an enum `BarcodeFormat`, defined in the library.

```dart

class _MyAppState extends State<MyApp> {

  final _qrBarCodeScannerDialogPlugin = QrBarCodeScannerDialog();
  String? code;

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: const Text('Plugin example app'),
		),
		body: Builder(builder: (context) {
          return Material(
            child: Center(
              child: ElevatedButton(
                  onPressed: () {
                    _qrBarCodeScannerDialogPlugin.getScannedQrBarCode(
                        context: context,
						onCode: (code) {
                          setState(() {
                            this.code = code;
						  });
					 });
				  },
				  child: Text(code ?? "Click me")),
			  ),
		    );
		  }),
		 ),
	  );
	}
}

```

## Android Integration
In order to use this plugin, please update the Gradle, Kotlin and Kotlin Gradle Plugin:

In ```android/build.gradle``` change ```ext.kotlin_version = '1.3.50'``` to ```ext.kotlin_version = '1.5.10'```

In ```android/build.gradle``` change ```classpath 'com.android.tools.build:gradle:3.5.0'``` to ```classpath 'com.android.tools.build:gradle:4.2.0'```

In ```android/gradle/wrapper/gradle-wrapper.properties``` change ```distributionUrl=https\://services.gradle.org/distributions/gradle-5.6.2-all.zip``` to ```distributionUrl=https\://services.gradle.org/distributions/gradle-6.9-all.zip```

In ```android/app/build.gradle``` change
```defaultConfig{```
  ```...```
  ```minSdkVersion 16```
```}``` to
```defaultConfig{```
  ```...```
  ```minSdkVersion 20```
```}```

### *Warning*
If you are using Flutter Beta or Dev channel (1.25 or 1.26) you can get the following error:

`java.lang.AbstractMethodError: abstract method "void io.flutter.plugin.platform.PlatformView.onFlutterViewAttached(android.view.View)"`

This is a bug in Flutter which is being tracked here: https://github.com/flutter/flutter/issues/72185

There is a workaround by adding `android.enableDexingArtifactTransform=false` to your `gradle.properties` file.

## iOS Integration
In order to use this plugin, add the following to your Info.plist file:
```
<key>io.flutter.embedded_views_preview</key>
<true/>
<key>NSCameraUsageDescription</key>
<string>This app needs camera access to scan QR codes</string>
```

## Web Integration

No need to update anything, plugin append the html contents to the DOM.