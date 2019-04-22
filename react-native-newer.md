---
title: react-native
date: 2017-10-17 21:16:14
tag: ['react-native']
categories: ['react-native']
---

## react-native 记

### css

```
"flex", 
"flexBasis", 
"flexDirection", 
"flexGrow", 
"flexShrink",  
"flexWrap",
"alignContent", 
"alignItems", 
"alignSelf", 
"justifyContent",
"aspectRatio",
"backfaceVisibility",
"backgroundColor", 
"color",
"borderBottomColor", 
"borderBottomLeftRadius", 
"borderBottomRightRadius", 
"borderBottomWidth", 
"borderColor", 
"borderLeftColor", 
"borderLeftWidth", 
"borderRadius", 
"borderRightColor", 
"borderRightWidth", 
"borderStyle", 
"borderTopColor", 
"borderTopLeftRadius", 
"borderTopRightRadius", 
"borderTopWidth", 
"borderWidth",
"bottom",
"decomposedMatrix",
"direction",
"display",
"elevation",
"fontFamily", 
"fontSize", 
"fontStyle", 
"fontVariant", 
"fontWeight",
"height",
"includeFontPadding",
"left",
"letterSpacing",
"lineHeight",
"margin", 
"marginBottom", 
"marginHorizontal", 
"marginLeft", 
"marginRight", 
"marginTop", 
"marginVertical",
"maxHeight", 
"maxWidth", 
"minHeight", 
"minWidth",
"opacity",
"overflow",
"overlayColor",
"padding", 
"paddingBottom", 
"paddingHorizontal", 
"paddingLeft", 
"paddingRight", 
"paddingTop", 
"paddingVertical",
"position",
"resizeMode",
"right",
"rotation",
"scaleX", 
"scaleY",
"shadowColor", 
"shadowOffset", 
"shadowOpacity", 
"shadowRadius",
"textAlign", 
"textAlignVertical", 
"textDecorationColor", 
"textDecorationLine", 
"textDecorationStyle", 
"textShadowColor", 
"textShadowOffset", 
"textShadowRadius",
"tintColor",
"top",
"transform", 
"transformMatrix", 
"translateX", 
"translateY",
"width",
"writingDirection",
"zIndex" 
```

### 配置 react-native-image-picker

#### github

[react-native-image-picker](https://github.com/marcshilling/react-native-image-picker)

#### 安装

> npm install react-native-image-picker@latest--save

#### 配置

##### ios

- 打开Xcode打开项目，点击根目录，右键选择 Add Files to 'XXX'，选中项目中的该路径下的文件即可
	
	> node_modules -> react-native-image-picker -> ios -> selectRNImagePicker.xcodeproj

- 添加 RNImagePicker.a

	> Build Phases -> Link Binary With Libraries 

- （ios10+）添加 NSPhotoLibraryUsageDescription 和 NSCameraUsageDescription：

	> 在 info.plist 中配置 NSPhotoLibraryUsageDescription 和 NSCameraUsageDescription

- 执行
	
	> react-native link react-native-image-picker

##### Android

- 修改 android/settings.gradle


	```
	include':react-native-image-picker'
	
	project(':react-native-image-picker').projectDir =newFile(settingsDir,'../node_modules/react-native-image-picker/android')
	```

- 修改 android/app/build.gradle
	
	```
	dependencies {
	
	        compile project(':react-native-image-picker')
	
	}
	```

- 修改 android/app/src/main/AndroidManifest.xml

	```
	<uses-permission android:name="android.permission.CAMERA" />
	<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
	```

- 修改 android/app/src/main/java/com/XXX/MainApplycation.java

	```
	import com.imagepicker.ImagePickerPackage;


	.........
	
	
	
	new ImagePickerPackage()
	```

#### 用法

```
import  ImagePicker from 'react-native-image-picker';

let options = {
    //底部弹出框选项
    title:'请选择',
    cancelButtonTitle:'取消',
    takePhotoButtonTitle:'拍照',
    chooseFromLibraryButtonTitle:'选择相册',
    quality:0.75,
    allowsEditing:true,
    noData:false,
    storageOptions: {
        skipBackup: true,
        path:'images'
    }
}

cameraAction = () =>{
	ImagePicker.showImagePicker(photoOptions,(response) =>{
		console.log('response'+response);
		if (response.didCancel){
			return
		}
	})
}
```
