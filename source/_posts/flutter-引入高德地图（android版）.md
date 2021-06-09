---
title: flutter 引入高德地图（android版）
date: 2021-04-01 22:02:48
author: Mr-xu
img: /images/3.jpg
top: false
cover: false
summary: 记录flutter配置高德地图时经历的痛，方便查阅
categories: flutter
tags:
  - 配置
---

# flutter 引入高德地图（android）

>配置搞得欲哭无泪

## 1.申请高德apikey

登录高德开发者平台，控制台-应用管理-创建应用

申请key时需要sha1（使用项目的打包文件 jks文件里的sha1）和packageName

## 2.下载sdk

>[官方sdk例子下载](https://lbs.amap.com/api/flutter/download)

## 3.配置

#### 将下载的官方包中的libs下的所有文件放置到项目的libs下

### 配置：
在项目的android/app文件下找到build.gradle， 在文件中找到sourceSets 标签，增加一项配置

  ``` javascript
  main{
    jniLibs.srcDirs=['libs'];
  }
  ```
在defaultConfig中加入：
  ``` javascript
  multiDexEnabled true
  manifestPlaceholders = [
      AMAP_KEY : "d6137d3d7c9aedfc4078db0b630613d4", /// 高德地图key
  ]
  ```
在dependencies中添加高德地图sdk
  ``` javascript
  implementation fileTree(include: ['*.jar'], dir: 'libs')
  ```



### 项目的 “AndroidManifest.xml” 文件中，添加如下代码:

#### 配置权限： application下面加入

  ``` javascript
  <!--允许程序打开网络套接字-->
  <uses-permission android:name="android.permission.INTERNET" />  
  <!--允许程序设置内置sd卡的写权限-->
  <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />    
  <!--允许程序获取网络状态-->
  <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" /> 
  <!--允许程序访问WiFi网络信息-->
  <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" /> 
  <!--允许程序读写手机状态和身份-->
  <uses-permission android:name="android.permission.READ_PHONE_STATE" />     
  <!--允许程序访问CellID或WiFi热点来获取粗略的位置-->
  <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" /> 
  ```

#### 引入插件：

1. 在Flutter工程的pubspec.yaml里的dependencies添加如下代码引入高德地图Flutter插件

  ``` javascript
  dependencies:
    amap_flutter_map: ^1.0.0
  ```

2.获取插件
  ``` bash
    flutter pub get
  ```

3.需要使用地图的dart文件中引入

  ``` javascript
  import 'package:amap_flutter_base/amap_flutter_base.dart'; // 基础包
  import 'package:amap_flutter_map/amap_flutter_map.dart';  // 插件包


  AMapController _mapController;
  // 项目中使用
    static const AMapApiKey amapApiKeys =
        AMapApiKey(androidKey: 'd6137d3d7c9aedfc4078db0b630613d4');

  Widget build(BuildContext context) {
    ///使用默认属性创建一个地图
    final AMapWidget map = AMapWidget(
      apiKey: amapApiKeys,
      onMapCreated: onMapCreated,
    );
    return Container(
        height: MediaQuery.of(context).size.height,
        width: MediaQuery.of(context).size.width,
        child: map,
    );
  }

  void onMapCreated(AMapController controller) {
      setState(() {
        _mapController = controller;
        getApprovalNumber();
      });
    }

  /// 获取审图号
  void getApprovalNumber() async {
    //普通地图审图号
    String mapContentApprovalNumber =
    await _mapController?.getMapContentApprovalNumber();
    //卫星地图审图号
    String satelliteImageApprovalNumber =
    await _mapController?.getSatelliteImageApprovalNumber();
  }
  ```
