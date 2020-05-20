# RedCorners.Forms.ZXing Changes

This library is a modified version of ZXing.Net.Mobile, with two major differences:
- It contains methods to take pictures, essentially making ZXingScannerView a proper Camera view,
- It does not include the ZXing DLL, and instead references its NuGet package,
- The structure of the project is different and only Android and iOS are supported.

# ZXing.Net.Mobile

[![Join the chat at https://gitter.im/Redth/ZXing.Net.Mobile](https://badges.gitter.im/Redth/ZXing.Net.Mobile.svg)](https://gitter.im/Redth/ZXing.Net.Mobile?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

![ZXing.Net.Mobile Logo](https://raw.github.com/Redth/ZXing.Net.Mobile/master/zxing.net.mobile_128x128.png)

ZXing.Net.Mobile is a C#/.NET library based on the open source Barcode Library: [ZXing (Zebra Crossing)](https://github.com/zxing/zxing), using the [ZXing.Net Port](https://github.com/micjahn/ZXing.Net).  It works with Xamarin.iOS, Xamarin.Android, Tizen, and UWP.  The goal of ZXing.Net.Mobile is to make scanning barcodes as effortless and painless as possible in your own applications.

[![Build Status](https://img.shields.io/endpoint.svg?url=https%3A%2F%2Factions-badge.atrox.dev%2Fredth%2FZXing.Net.Mobile%2Fbadge&style=flat)](https://actions-badge.atrox.dev/redth/ZXing.Net.Mobile/goto)
[![NuGet](https://img.shields.io/nuget/v/ZXing.Net.Mobile.svg)](https://www.nuget.org/packages/ZXing.Net.Mobile/)
[![NuGet](https://img.shields.io/nuget/dt/ZXing.Net.Mobile.svg)](https://www.nuget.org/packages/ZXing.Net.Mobile/)

### Usage
The simplest example of using ZXing.Net.Mobile looks something like this:

```csharp  
buttonScan.Click += (sender, e) => {

	#if __ANDROID__
	// Initialize the scanner first so it can track the current context
	MobileBarcodeScanner.Initialize (Application);
  	#endif
  	
	var scanner = new ZXing.Mobile.MobileBarcodeScanner();

	var result = await scanner.Scan();

	if (result != null)
		Console.WriteLine("Scanned Barcode: " + result.Text);
};
```


#### Xamarin Forms
For Xamarin Forms there is a bit more setup needed.  You will need to initialize the library on each platform in your platform specific app project.

### Features
- Xamarin.iOS
- Xamarin.Android
- Simple API - Scan in as little as 2 lines of code!
- Scanner as a View - UIView (iOS) / Fragment (Android) / Control (WP)

### Custom Overlays
By default, ZXing.Net.Mobile provides a very simple overlay for your barcode scanning interface.  This overlay consists of a horizontal red line centered in the scanning 'window' and semi-transparent borders on the top and bottom of the non-scanning area.  You also have the opportunity to customize the top and bottom text that appears in this overlay.

If you want to customize the overlay, you must create your own View for each platform.  You can customize your overlay like this:

```csharp
var scanner = new ZXing.Mobile.MobileBarcodeScanner();
scanner.UseCustomOverlay = true;
scanner.CustomOverlay = myCustomOverlayInstance;
var result = await scanner.Scan();
//Handle result
```

Keep in mind that when using a Custom Overlay, you are responsible for the entire overlay (you cannot mix and match custom elements with the default overlay).  The *ZxingScanner* instance has a *CustomOverlay* property, however on each platform this property is of a different type:

- Xamarin.iOS => **UIView**
- Xamarin.Android => **View**

All of the platform samples have examples of custom overlays.
