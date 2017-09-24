---
title: Camera
description: "NativeScript Documentation: Camera"
position: 20
slug: camera
previous_url: /camera
---

# Camera

# 相机

## Overview

## 概述

Almost every mobile application needs the option to capture, save and share images. The NativeScript camera plugin was designed for the first two parts of the job (taking a picture and optionally saving to device storage).

几乎所有的移动端应用都可能需要使用相机来进行拍照，用以保存或分享图片的功能。NativeScript的相机模块现在能够实现前面两个功能，即拍取照片，并可以选择是否将图片保存到本地存储。

### Installation

### 安装

Navigate to project folder and run NativeScript-CLI command 

在项目文件夹的根目录下运行NativeScript-CLI命令

``` 
tns plugin add nativescript-camera
``` 

Plugin could be added as a standard npm dependency running command 

当然也能够以npm模块依赖的方式引入相机模块

``` 
npm install nativescript-camera --save 
``` 

> Note: the `--save` flag will add the plugin as dependency in your package.json file

> 注意：`--save`参数会将模块名和版本号添加到`package.json`文件中`dependencies`部分。

### Requesting permissions

### 权限申请

Newer API levels of Android and iOS versions are requiring explicit permissions in order the application
to have access to the camera and to be able to save photos to the device. Once the user has granted permissions the camera module can be used.

移动应用在较新版本的Android和iOS设备需要向系统申请特定权限之后才能够自由的使用相机以及保存图片到本地存储。 一旦用户同意了授权，相机模块的功能就可以自由使用了。

```
camera.requestPermissions();
```

> Note: Older versions won't be affected by the usage of the requestPermissions method.

> 注意：在旧版本中的设备中，调用`requestPermissions`方法不会产生负面影响。

### Using the camera module to take a picture

### 拍取照片

Using the camera module is relatively simple. 
However, there are some points that need a little bit more explanation.

相机模块的使用是非常简单方便的。不过，本文还是会对某些要点进行详细的解释的。

In order to use the camera module, just require it, as shown in Example 1:

正如例1所示，引入相机模块，即可进行使用了。

> Example 1: Require camera module in the application

> 例1：在应用中引入模块

``` JavaScript
var camera = require("nativescript-camera");
```
``` TypeScript
import * as camera from "nativescript-camera";
```

Then you are ready to use it:

然后就可以使用了：

> Example 2: How to take a picture and to receive image asset

> 例2： 拍取照片，获取图片资源

``` JavaScript
var imageModule = require("ui/image");
camera.takePicture()   
    .then(function (imageAsset) {
        console.log("Result is an image asset instance");
        var image = new imageModule.Image();
        image.src = imageAsset;
    }).catch(function (err) {
        console.log("Error -> " + err.message);
    });
```
``` TypeScript
import { Image } from "ui/image";
camera.takePicture()
    .then((imageAsset) => {
        console.log("Result is an image asset instance");
        let image = new Image();
        image.src = imageAsset;
    }).catch((err) => {
        console.log("Error -> " + err.message);
    });
```

The code in __Example 2__ will start the native platform camera application. After taking the picture and tapping the button `Save` (Android) or `use image` (iOS), the promise will resolve the `then` part and image asset will be set as `src` of the `ui/image` control.

__例2__中的代码将会调用系统原生的相机应用。拍照完成后，点击按钮（Android上是`保存／Save`，iOS是`使用照片/use image`）之后，promise会执行`then`处的函数，图片资源将会作为变量`src`传递给`ui/image`使用。

### Using the options to take memory efficient picture

### 通过配置选项来节约内存开销

__Example 2__ shows how to take a picture using the NativeScript camera module. However, it takes a huge image (even mid-level devices has a 5MP camera, which results in a image 2580x2048, which in bitmap means approximately 15 MB). In many cases you don't need such a huge picture to show an image with 100x100 size, so taking a big picture is just a waste of memory. The camera takePicture() method accepts an optional parameter that could help in that case. With that optional parameter, you could set some properties like:

__例2__展示了如何使用NativeScript的相机模块来拍照。不过，这个方法拍取的照片非常大（即使是中等设备也有500百万像素的相机，拍出来的照片尺寸将会是2580x2048，这也就意味着大约15MB的位图存储）。在很多情况下，你可能只需要相对较小尺寸的图片，不需要拍取这么大一张图片，所以这简直就是对内存的浪费。为了解决这种情况，`takePicture()`方法接受额外的可选参数，`options`。`options`参数包含以下几种属性：

* __width__: The desired width of the picture (in device independent pixels).

  __width__: 图片的宽，单位DPI，设备独立像素（`device independent pixels`，见下文解释）.

* __height__: The desired height of the picture (in device independent pixels).

  __height__: 图片的高，单位DPI，设备独立像素（见下文解释）. 

* __keepAspectRatio__: A boolean parameter that indicates if the aspect ratio should be kept.

  __keepAspectRatio__: 是否保持高宽比，布尔值，true表示保持原有的高宽比，false表示相反。

* __saveToGallery__: A boolean parameter that indicates if the taken photo will be saved in "Photos" for Android and in "Camera Roll" in iOS

  __saveToGallery__: 是否保存到图库，布尔值，true时将会把照片保存到图库（Android为Photos文件夹，iOS则为Camera Roll）。

What does `device independent pixels` mean? The NativeScript layout mechanism uses device-independent pixels when measuring UI controls. This allows you to declare one layout and this layout will look similar to all devices (no matter the device's display resolution). In order to get a proper image quality for high resolution devices (like iPhone retina and Android Full HD), camera will return an image with bigger dimensions. For example, if we request an image that is 100x100, on iPhone 6 the actual image will be 200x200 (since its display density factor is 2 -> 100\*2x100\*2).

`device independent pixels（DPI）`是什么？ NativeScript的布局机制在展示UI控件的时候使用了设备独立像素（DPI）进行渲染。使用DPI可以让你定义的UI布局在不同分辨率的设备的展示中相差无几。在诸如iPhone Retina或Android Full HD等高分辨率的设备中，相机模块获取的照片将会有更大的尺寸。比如我们想要一张100x100的图片，在iPhone6中，由于DPI为2，所以图片的实际尺寸将会是100\*2 x 100\*2。

Setting the `keepAspectRatio` property could result in a different than requested width or height. The camera will return an image with the correct aspect ratio but generally only one (from width and height) will be the same as requested; the other value will be calculated in order to preserve the aspect of the original image.

设置`keepAspectRatio`属性为`true`时可能会导致图片最后具有不同与options中要求的长度或者宽度值。相机模块将会返回一张具有原有高宽比的的图片，不过这个图片的两个方向的尺寸将会只有一个是跟`options`中要求的一致，另一个则是根据高宽比计算而得到。

__Example 3__ shows how to use the options parameter:

__例3__演示了如何配置`options`参数

> Example 3: How to setup `width`, `height`, `keepAspectRatio` and `saveToGallery` properties for the camera module

> 例3: 如何配置`options`参数中的`width`，`height`，`keepAspectRatio`和`saveToGallery`属性

``` JavaScript
var imageModule = require("ui/image");

var options = { width: 300, height: 300, keepAspectRatio: false, saveToGallery: true };
camera.takePicture(options)   
    .then(function (imageAsset) {
        console.log("Size: " + imageAsset.options.width + "x" + imageAsset.options.height);
        console.log("keepAspectRatio: " + imageAsset.options.keepAspectRatio);
        console.log("Photo saved in Photos/Gallery for Android or in Camera Roll for iOS");
    }).catch(function (err) {
        console.log("Error -> " + err.message);
    });
```
``` TypeScript
import { Image } from "ui/image";

var options = { width: 300, height: 300, keepAspectRatio: false, saveToGallery: true };
camera.takePicture(options)
    .then((imageAsset) => {
        console.log("Size: " + imageAsset.options.width + "x" + imageAsset.options.height);
        console.log("keepAspectRatio: " + imageAsset.options.keepAspectRatio);
        console.log("Photo saved in Photos/Gallery for Android or in Camera Roll for iOS");
    }).catch((err) => {
        console.log("Error -> " + err.message);
    });
```

### Check if the device has available camera

### 检查设备是否有用的相机硬件

The first thing that the developers should check if the device has an available camera. The method isAvaialble will return true if the camera hardware is ready to use or false if otherwise.

在使用相机模块时，开发者需要做的第一件事情就是检查设备是否有可用的相机硬件。如果设备有可用的相机硬件，方法`isAvailable()` 将会返回`true`，否则返回`false`。

```
var isAvailable = camera.isAvailable(); 
```

> Note: This method will return false when used in iOS simulator (as the simulator does not have camera hardware)

> 注意：在mac上的iOS模拟器中使用该方法会返回`false`，因为根本不存在相应的相机硬件。
