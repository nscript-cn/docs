---
title: Location
description: How to work with geographical location data in NativeScript.
position: 10
slug: location
previous_url: /location
---

# Location

# 地理位置

> **IMPORTANT:** Starting with NativeScript 1.5.0, the built-in Location module is deprecated. To implement geolocation in your apps, use the `nativescript-geolocation` plugin, available via npm. This plugin provides an API similar to the [W3C Geolocation API](http://dev.w3.org/geo/api/spec-source.html). 

> **重要信息:** 内建的地理位置模块将从NativeScript 1.5.0版本开始被弃用。若要在应用中实现地理位置处理功能, 可用npm安装`nativescript-geolocation`插件。该插件提供了与[W3C Geolocation API](http://dev.w3.org/geo/api/spec-source.html)相仿的API。

The most important difference between the deprecated module and the new plugin is that location monitoring via the plugin returns an `id` that you can use to stop location monitoring. The `nativescript-geolocation` plugin also uses an accuracy criteria approach to deliver geolocation. This means that getting a location is powered by the most accurate location provider that is available. For example, if a GPS signal is available and the GPS provider is enabled, the plugin uses GPS; if GPS is not connected, the device falls back to other available providers such as Wi-Fi networks or cell towers).

被弃用的模块和新启用的插件之间最大的区别在于，通过插件获取到的位置监控器返回一个`id`，这个`id`可以用来停止位置监控器。此外，`nativescript-geolocation`插件还通过使用一种高精度标准的方式来提供地理位置信息。这意味着获取的位置信息由当前可用的最精确的位置提供者提供。例如，如果可以获取到GPS信号而且GPS提供者被启用，则插件使用GPS；如果GPS无法连接，则设备使用其他可用的提供者，例如Wi-Fi网络或者蜂窝网络信号塔。

This approach does not limit location monitoring only to a specific location provider; it can still work with all of them.

但这种方式并不会把位置监控器限定为某个特定的位置提供者，而是仍使用全部的。

You might want to start with this [example](https://github.com/nsndeck/locationtest), which demonstrates how to use the `nativescript-geolocation` plugin.

你可能会希望通过一个[示例](https://github.com/nsndeck/locationtest)来学会如何使用`nativescript-geolocation`插件。

To make the plugin available in your app, run the following command:

为了在你的App中使用这个插件，请执行以下的命令：

```Shell
tns plugin add nativescript-geolocation
```

```Shell
tns plugin add nativescript-geolocation
```

To import the module in your code, use:

之后在代码中引入插件：

{% nativescript %}
```JavaScript
var geolocation = require("nativescript-geolocation");
```

{% endnativescript %}
```TypeScript
import { isEnabled, enableLocationRequest, getCurrentLocation, watchLocation, distance, clearWatch } from "nativescript-geolocation";
```

## Getting information about a location service

## 获取和位置服务相关的信息

NativeScript has a universal way to check if location services are turned on&mdash;the `isEnabled` method. The method returns a Boolean value (true if the location service is enabled).

在NativeScript中使用了`isEnabled`这个通用方法来检查位置服务是否开启。方法会返回一个`Boolean`类型的值(如果位置服务已开启则返回`true`)。

> **NOTE:** For Android, `isEnabled` checks if the location service is enabled (any accuracy level). For iOS, the method checks if the location service is enabled for the application in foreground or background mode.

> **注意:** 在Android平台下，`isEnabled`检测的是（任意精度等级）的位置服务是否启用。而在iOS中，这个方法检查的是应用在前台或者后台等任意状态下位置服务是否启用。

## Requesting permissions to use location services

## 获取使用位置服务的权限

By default, the `nativescript-geolocation` plugin adds the required permissions in `AndroidManiest.xml` for Android and `Info.plist` for iOS. For iOS, the plugin adds two dummy string values which serve as the message when the platform asks for permission to use location services. You can edit this message later. 

`nativescript-geolocation`会默认在Android平台下的`AndroidManiest.xml`和iOS平台下的`Info.plist`中添加所需的权限。此外，在iOS平台下，插件添加了两个空字符串作为提示语句，它们将会在平台向用户请求位置服务权限时使用。你可以在之后修改它。

After you install the plugin, you can request to use location services in the app with the code in __Example 1__:

在完成插件的安装后，你可以使用__样例1__中的代码来请求使用位置服务。

> Example 1: How to enable location service on a device

> 样例1：如何在设备中启用位置服务

{% nativescript %}
```XML
<Page> 
    <StackLayout>
        <Button text="enable Location" tap="enableLocationTap"/>
    </StackLayout>
</Page>
```
```JavaScript
function enableLocationTap(args) {
    if (!geolocation.isEnabled()) {
        geolocation.enableLocationRequest();
    }
}
exports.enableLocationTap = enableLocationTap;
```
{% endnativescript %}
{% angular %}
```XML
<StackLayout>
    <Button text="enable Location" (tap)="enableLocationTap()"></Button>
</StackLayout>
```
{% endangular %}
```TypeScript
{% nativescript %}export function {% endnativescript %}public {% angular %}{% endangular %}enableLocationTap() { 
    if (!isEnabled()) {
        enableLocationRequest();
    }
}
```

## Getting location

## 获取定位

You can get location with `getCurrentLocation` or with `watchLocation`. Using `distance`, you can obtain the distance between two locations.

你可以通过`getCurrentLocation`或`watchLocation`方法来获取位置信息，并通过`distance`方法来获取两个位置之间的距离。

* [getCurrentLocation](#getcurrentlocation)
* [watchLocation](#watchlocation)
* [distance](#distance)

### `getCurrentLocation`

This method gets a single location. It accepts the `location options` parameter. 

此方法用来获取单个位置信息，它接受`location options`参数。 

`getCurrentLocation` returns a `Promise<Location>` where `Location` and `location options` are defined as follows.

`getCurrentLocation`方法返回`Promise<Location>`。对`Location`和`location options`的定义如下。

#### Class: location  
#### 类: location  
A data class that encapsulates common properties for a geolocation.

一个包含地理位置基本信息的数据类。

##### Instance properties
##### 实例属性

Property | Type | Description
---|---|---
`latitude` | Number | The latitude of the geolocation, in degrees.
`longitude` | Number | The longitude of the geolocation, in degrees.
`altitude` | Number | The altitude (if available), in meters above sea level.
`horizontalAccuracy` | Number | The horizontal accuracy, in meters.
`verticalAccuracy` | Number | The vertical accuracy, in meters.
`speed` | Number | The speed, in meters/second over ground.
`direction` | Number | The direction (course), in degrees.
`timestamp` | Object | The time at which this location was determined.
`android` | Object | The Android-specific [location](http://developer.android.com/reference/android/location/Location.html) object.
 `ios` | CLLocation | The iOS-specific [CLLocation](https://developer.apple.com/library/ios/documentation/CoreLocation/Reference/CLLocation_Class/) object.


属性 | 类型 | 描述
---|---|---
`latitude` | Number | 纬度，以度数（deg）为单位。
`longitude` | Number | 经度，以度数（deg）为单位。
`altitude` | Number | 海拔（如果可用），以米为单位。
`horizontalAccuracy` | Number | 水平精度，以米为单位。
`verticalAccuracy` | Number | 垂直精度，以米为单位。
`speed` | Number | 速度，以米每秒为单位。
`direction` | Number | 方向（航向），以度数（deg）为单位。
`timestamp` | Object | 刚刚取到此位置时的时间戳。
`android` | Object | Android特有[位置](http://developer.android.com/reference/android/location/Location.html)对象。
 `ios` | CLLocation | iOS特有[位置](https://developer.apple.com/library/ios/documentation/CoreLocation/Reference/CLLocation_Class/)对象。

#### Interface: options  
#### 接口: options  
Provides options for location monitoring.

为位置检测提供的选项。

##### Properties
##### 属性

Property | Type | Description
---|---|---
`desiredAccuracy` | Number | (Optional) Specifies desired accuracy in meters. NativeScript has a special enum [Accuracy](http://docs.nativescript.org/api-reference/modules/_ui_enums_.accuracy.html) that helps to make code more readable. Defaults to `Accuracy.any`. Such accuracy could be achieved with only wifi and assist GPS from network provider, therefore does not put additional pressure on battery consumption. In order to use high accuracy (requires GPS sensor) set this option to `Accuracy.high`.
`updateDistance` | Number | (Optional) Updates distance filter in meters. Specifies how often to update. Default on iOS is no filter, on Android it is 0 meters.
`minimumUpdateTime` | Number | (Optional) Specifies the minimum time interval between location updates, in milliseconds. Ignored on iOS.
`maximumAge` | Number | (Optional) Filters locations by how long ago they were received, in milliseconds. For example, if the `maximumAge` is 5000, you will get locations only from the last 5 seconds. 
`timeout` | Number | (Optional) Specifies how long to wait for a location, in milliseconds.

属性 | 类型 | 描述
---|---|---
`desiredAccuracy` | Number | (可选的)指定所需的精度，以米为单位。NativeScript有一个特殊的枚举类型[Accuracy](http://docs.nativescript.org/api-reference/modules/_ui_enums_.accuracy.html)来帮助提高代码的可读性。默认设为`Accuracy.any`。这样的精度可以通过WiFi和辅助GPS来实现，不会对电池消耗造成额外的压力。若要使用高精度模式（需要GPS传感器）请将其设置为`Accuracy.high`。
`updateDistance` | Number | (可选的) 更新距离筛选器，以米为单位。指定更新的频率。在iOS中无法筛选，在Android中默认为0米。
`minimumUpdateTime` | Number | (可选的) 设置位置信息更新的最小间隔时间，以毫秒为单位。在iOS中会被忽略。
`maximumAge` | Number | (可选的) 筛选多少时间内我们获取到的位置信息，以毫秒为单位。例如，如果`maximumAge`设置为5000，你只会获取到5秒内获取到的位置数据。
`timeout` | Number | (可选的) 设置获取位置的最大等待时间，以毫秒为单位。

> Example 2: How to get current location

> 样例2：如何获取当前位置

{% nativescript %}
```XML
<Page>
    <StackLayout>
        <Button text="Get Current Location" tap="buttonGetLocationTap"/>
    </StackLayout>
</Page>
```
```JavaScript
function buttonGetLocationTap(args) {
	var location = geolocation.getCurrentLocation({desiredAccuracy: 3, updateDistance: 10, maximumAge: 20000, timeout: 20000}).
	then(function(loc) {
		if (loc) {
			console.log("Current location is: " + loc);
		}
	}, function(e){
		console.log("Error: " + e.message);
	});
}
exports.buttonGetLocationTap = buttonGetLocationTap;
```
{% endnativescript %}
{% angular %}
```XML
<StackLayout>
    <Button text="Get Current Location" (tap)="buttonGetLocationTap()"></Button>
</StackLayout>
```
{% endangular %}
```TypeScript
{% nativescript %}export function {% endnativescript %}public {% angular %}{% endangular %}buttonGetLocationTap() {
	var location = getCurrentLocation({desiredAccuracy: 3, updateDistance: 10, maximumAge: 20000, timeout: 20000}).
	then(function(loc) {
		if (loc) {
			console.log("Current location is: " + loc);
		}
	}, function(e){
		console.log("Error: " + e.message);
	});
}
```

### `watchLocation`

With this method, location watching does not stop automatically until the `clearWatch` method is called. You might need to use this method in apps which require a GPS log or active location tracking. 

使用此方法会让位置监视一直生效，直到你调用了`clearWatch`方法才会停止。在App中可能需要通过它来实现GPS日志获取或者实时位置跟踪。

> Example 3: How to handle location change event

> 样例3：如何处理位置发生变化的事件

{% nativescript %}
```XML
<Page>
    <StackLayout>
		<Button row="2" text="start monitoring" tap="buttonStartTap"/>
		<Button row="3" text="stop monitoring" tap="buttonStopTap"/>
    </StackLayout>
</Page>
```
``` JavaScript
function buttonStartTap() {
	watchId = geolocation.watchLocation(
	function (loc) {
		if (loc) {
			console.log("Received location: " + loc);
		}
	}, 
	function(e){
		console.log("Error: " + e.message);
	}, 
	{desiredAccuracy: 3, updateDistance: 10, minimumUpdateTime : 1000 * 20}); // should update every 20 sec according to google documentation this is not so sure.
}
exports.buttonStartTap = buttonStartTap;

function buttonStopTap() {
	if (watchId) {
		geolocation.clearWatch(watchId);
	}
}
exports.buttonStopTap = buttonStopTap;
```
{% endnativescript %}
{% angular %}
```XML
<StackLayout>
    <Button row="2" text="start monitoring" (tap)="buttonStartTap()"></Button>
    <Button row="3" text="stop monitoring" (tap)="buttonStopTap()"></Button>
</StackLayout>
```
{% endangular %}
``` TypeScript
{% nativescript %}export function {% endnativescript %}public {% angular %}{% endangular %}buttonStartTap() {
	watchId = watchLocation(
	function (loc) {
		if (loc) {
			console.log("Received location: " + loc);
		}
	}, 
	function(e){
		console.log("Error: " + e.message);
	}, 
	{desiredAccuracy: 3, updateDistance: 10, minimumUpdateTime : 1000 * 20}); // Should update every 20 seconds according to Googe documentation. Not verified.
}

{% nativescript %}export function {% endnativescript %}public {% angular %}{% endangular %}buttonStopTap() {
	if (watchId) {
		clearWatch(watchId);
	}
}
```

### `distance`

This method lets you measure the distance between two locations in meters.

此方法用来计算两个位置之间距离，以米为单位。

> Example 4: How to get distance between to two location

> 样例4：获取两个位置之间的距离

{% nativescript %}
```JavaScript
function getDistance(loc1, loc2) {
    console.log("Distance between loc1 and loc2 is: " + geolocation.distance(loc1, loc2));
}
```
{% endnativescript %}
```TypeScript
function getDistance(loc1, loc2) {
    console.log("Distance between loc1 and loc2 is: " + distance(loc1, loc2));
}
```

## See Also

## 其他参考

* [NativeScript Plugins](http://docs.nativescript.org/plugins/plugins)
* [Location Module (Deprecated)](http://docs.nativescript.org/api-reference/modules/_location_.html)
* [NativeScript-Geolocation in NPM](https://www.npmjs.com/package/nativescript-geolocation)
