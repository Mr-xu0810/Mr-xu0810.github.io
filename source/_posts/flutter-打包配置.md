---
title: flutter 打包配置
date: 2021-04-05 19:25:58
author: Mr-xu
img: /images/2.jpg
top: false
cover: false
summary: 记录flutter打包配置过程，方便后续查阅
categories: flutter
tags:
  - 配置
---

# flutter 打包配置

### 生成jks：打包用的keystore

```bash
keytool -genkey -v -keystore/Users/fei/keystore/test.jks -keyalg RSA -keysize 2048 -validity 10000 -alias test
```

/Users/fei/keystore/test.jks 生成的文件路径及jks文件，test  别名

### 查看sha1:

```bash
keytool -v -list -keystore 【jks文件路径（/Users/fei/keystore/test.jks）】 
输入密码后可获取sha1码
```
![](/images/screenshot/view_sha1.jpg)

### 在Android目录下新建key.properties文件；

内容如下：

```bash
storePassword=123456
keyPassword=123456
keyAlias=test
storeFile=/Users/fei/keystore/test.jks
```

### 修改app目录下的build.gradle:

#### 在android之前添加：

```bash
def keyProperties=new Properties()
def keyPropertiesFile=rootProject.file("key.properties")
if(keyPropertiesFile.exists()) {
	keyProperties.load(new FileInputStream(keyPropertiesFile))
}
```

#### 在buildTypes  上面添加 signingConfigs:

```bash
signingConfigs{
    release{
        keyAlias keyProperties['keyAlias']
        keyPassword keyProperties['keyPassword']
        storeFile keyProperties['storeFile'] ? file(keyProperties['storeFile']) : null
        storePassword keyProperties['storePassword']
    }
}
```

#### 调整buildTypes：

```bash
buildTypes {
        release {
            // TODO: Add your own signing config for the release build.
            // Signing with the debug keys for now, so `flutter run --release` works.
            signingConfig signingConfigs.release
            //关闭混淆, 否则在运行release包后可能出现运行崩溃， TODO后续进行混淆配置
            minifyEnabled false //删除无用代码
            shrinkResources false //删除无用资源
        }
        debug {
            signingConfig signingConfigs.release
            //关闭混淆, 否则在运行release包后可能出现运行崩溃， TODO后续进行混淆配置
            minifyEnabled false //删除无用代码
            shrinkResources false //删除无用资源
        }
    }
```

### 配置完成，运行命令打包：

```bash
flutter build apk
```

等待完成即可