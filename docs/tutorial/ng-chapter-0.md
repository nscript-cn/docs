---
title: Building Apps with NativeScript and Angular
description: Learn the basics of how NativeScript and Angular work, how to set up your system, and how to create your first app
position: 1
guide: true
environment: angular
---

# Building Apps with NativeScript and Angular

# 使用NativeScript和Angular来构建应用

Welcome to the NativeScript & Angular getting started guide. In this hands-on tutorial, you’ll build a cross-platform iOS and Android app from scratch.

欢迎来到NativeScript与Angular快速上手教程。在这个实战教程中，你将会从头开始构建一个跨iOS与Android平台的App。

## Table of contents

## 目录

- [0.1: What is NativeScript? What is Angular?](#01-what-is-nativescript-what-is-angular)
- [0.1: 什么是NativeScript?什么是Angular?](#01-what-is-nativescript-what-is-angular)
- [0.2: Prerequisites](#02-prerequisites)
- [0.2: 前置知识](#02-prerequisites)
- [0.3: Installation](#03-installation)
- [0.3: 安装](#03-installation)

> **TIP**: If you’re a video learner, the third-party site NativeScripting has a [free video course](https://nativescripting.com/course/nativescript-with-angular-getting-started-guide) that walks you through this guide step by step.

> **提示**: 如果你是一位视频方式学习者，第三方网站NativeScripting有一个[免费的视频课程](https://nativescripting.com/course/nativescript-with-angular-getting-started-guide)，它将会一步一步引导你完成本教程。

## 0.1: What is NativeScript? What is Angular?

## 0.1: 什么是NativeScript? 什么是Angular?

<div class="intro-box">
  <img src="../img/cli-getting-started/angular/chapter0/NativeScript_logo.png" class="plain" alt="NativeScript logo">
  <p><a href="https://www.nativescript.org/">NativeScript</a> is a free and open source framework for building native iOS and Android apps using JavaScript and CSS. NativeScript renders UIs with the native platform’s rendering engine—no <a href="http://developer.telerik.com/featured/what-is-a-webview/">WebViews</a>—resulting in native-like performance and UX.</p>
</div>

<div class="intro-box">
  <img src="../img/cli-getting-started/angular/chapter0/NativeScript_logo.png" class="plain" alt="NativeScript logo">
  <p><a href="https://www.nativescript.org/">NativeScript</a>是一个免费、开源的框架，仅通过使用JavaScript和CSS就得以构建原生的iOS以及Android应用。NativeScript使用原生平台的渲染引擎来渲染用户界面—而不是<a href="http://developer.telerik.com/featured/what-is-a-webview/">WebViews</a>—从而获取到接近原生的性能和用户体验。</p>
</div>

<div class="intro-box">
  <img src="../img/cli-getting-started/angular/chapter0/Angular_logo.png" class="plain" alt="Angular logo">
  <p><a href="https://angular.io/">Angular</a> is one of the most popular open source JavaScript frameworks for application development. The latest version of Angular makes it possible to use the framework outside of a web browser, and developers at <a href="https://www.progress.com/">Progress</a>—the company that created and maintains NativeScript—<a href="http://angularjs.blogspot.com/2015/12/building-mobile-apps-with-angular-2-and.html">worked closely with developers at Google for over a year</a> to make Angular in NativeScript a reality.</p>
</div>

<div class="intro-box">
  <img src="../img/cli-getting-started/angular/chapter0/Angular_logo.png" class="plain" alt="Angular logo">
  <p><a href="https://angular.io/">Angular</a>是用于构建应用的最流行的开源JavaScript框架之一。最新版本的Angular可以在浏览器环境外使用，经过<a href="https://www.progress.com/">Progress</a>—创建和维护NativeScript的公司—<a href="http://angularjs.blogspot.com/2015/12/building-mobile-apps-with-angular-2-and.html">的开发者与Google的开发者一年多的紧密合作，</a>使得在NativeScript中使用Angular成为现实。</p>
</div>

The result is a software architecture that allows you to build mobile apps using the same framework—and in some cases the same code—that you use to build Angular web apps, with the performance you’d expect from native code. Let’s look at how it all works by building an app.

这所带来的结果就是能够把用于构建Angular Web应用的框架——或者代码——使用到构建移动应用中去，同时得到你所期望的原生代码的性能。现在我们来了解如何使用它来构建一个应用。

> **NOTE**: If you spot any issues while completing this guide, let us know on our [Angular GitHub repo](https://github.com/NativeScript/nativescript-angular/issues).

> **注意**: 如果在完成引导的过程中遇到什么问题，请提交issue到[Angular GitHub repo](https://github.com/NativeScript/nativescript-angular/issues)让我们知道。

## 0.2: Prerequisites

## 0.2: 前置知识

This guide assumes that you have some basic knowledge of JavaScript, CSS, and your development machine’s terminal. More specifically:

这份教程会假设你已经拥有了一些JavaScript、CSS和终端的一些基础知识。详细的有:

* **JavaScript**: You should know basic JavaScript concepts, such as how functions, if statements, and loops work.
* **JavaScript**: 了解JavaScript的基础概念，例如如何使用函数，if语句和循环。
* **CSS**: You should know how to write simple CSS selectors, and know how to apply CSS rules as name/value pairs.
* **CSS**: 知道如何写一些简单的CSS选择器, 同时也知道如何使用CSS规则例如键值对。
* **The terminal**: You should know how to open a terminal or command-line prompt on your development machine, how to change directories, and how to execute commands.
* **终端**: 需要知道如何在你的开发设备上打开终端或者命令行工具，如何切换路径以及如何执行命令。
* **A text editor or IDE**: You should know the basics of your text editor or IDE of choice. You can use any text editor to build NativeScript apps, however, for the best possible experience you may want an editor with built-in TypeScript support, such as [Visual Studio Code](https://code.visualstudio.com/).
* **一个文本编辑器或者集成开发环境**: 对你所选的文本编辑器或者集成开发环境有基本的了解。你可以使用任何一个文本编辑器来构建NativeScript应用，但是通过经验来看你最好选择一个内建TypeScript支持的编辑器例如[Visual Studio Code](https://code.visualstudio.com/)。

This guide will _not_ assume you have any knowledge of Angular or TypeScript. When background Angular or TypeScript expertise will help you understand a concept, this guide will link you to the appropriate places in the [Angular](https://angular.io/docs/ts/latest/) or [TypeScript](http://www.typescriptlang.org/Handbook) documentation.

这份引导_不_假设你有任何关于Angular或者TypeScript的知识。当需要Angular或TypeScript的专业知识作为背景帮你了解一些概念的时候，这份引导将会给出一个适当的[Angular](https://angular.io/docs/ts/latest/)或[TypeScript](http://www.typescriptlang.org/Handbook)文档链接供你参考。

## 0.3: Installation

## 0.3: 安装

In order to start this tutorial you need to have the NativeScript CLI (command-line interface) installed on your development machine, which you can do using the link below.

在开始教程前需要将NativeScript CLI(命令行界面)安装到你的开发设备上。可以按照下面提供的链接完成安装。

* [Complete the NativeScript installation guide](/start/quick-setup)
* [引导你完成NativeScript的安装](/start/quick-setup)

> **TIP**: Setting up your machine for native development can be tricky, especially if you’re new to mobile development. If you get stuck, or if you have questions while going through these instructions, the [NativeScript community forum](http://forum.nativescript.org/) is a great place to get help.

> **提示**: 配置原生开发的过程中可能会有奇怪的问题，特别是对移动开发陌生的情况下。如果你遇到困难，或者在学习过程中碰到一些问题，[NativeScript community forum](http://forum.nativescript.org/)将会是个获取帮助的好去处。

With that out of the way, let’s get started building apps with NativeScript!

搞定以上这些，就让我们开始用NativeScript构建应用吧!

<div class="next-chapter-link-container">
  <a href="ng-chapter-1">Continue to Chapter 1—Getting Up and Running</a>
</div>

<div class="next-chapter-link-container">
  <a href="ng-chapter-1">继续第一章—开始和运行</a>
</div>
