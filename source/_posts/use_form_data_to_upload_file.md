---
title: angular1文件上传
date: 2017-04-02 00:19:14
tags: ["angular1", "file-upload", "form-data"]
---


> Q: post上传文件并带参数。
> 
> A: 解决方法有很多种，常用form表单。我们主要说使用 angular1 发送 ajax 。


##### 1. angular1 $http.post

后台需要传过去一个文件列表，传给后台 form-data

* 文件 list name 为 file
* 参数 name 为 type

<!--more-->

在服务中封装了一个方法，相同的需求就只需要调用 http_form_file_data 方法。

```

/**
 * 这一步非常重要
 * 设置 Content-Type 为 undefined ，浏览器会自动填充
 * ！！！千万不要设置 Content-Type 为 multipart/form-data !!!
 * /
var postCfgFile = {

	headers: {'Content-Type': undefined},
	
	/**
	 * 返回函数本身的第一个参数
	 * /
	transformRequest: angular.identity
}


/**
 * post form data格式的带文件数据
 * @param str
 * @param obj obj是一个自定义对象，
 * @returns {Promise}
 */
http_form_file_data: function (str, obj) {

	var deferred = $q.defer();
	
	var data = new FormData();

	angular.forEach(obj, function (value, key) {

		/**
		 * 文件的 key 是 file ，多个文件需要全部 append 到 FormData 里
		if (key == 'file') {
			
			angular.forEach(value, function (file) {

				data.append(key, file);
			
			});
			
			return;
		}

		data.append(key, value);
	});

	$http
		.post(str, data, postCfgFile)
		.success(function (data) {

			deferred.resolve(data);
		
		});
		
	return deferred.promise;

}
```
如果设置 Content-Type 为 multipart/form-data ，后台会抛出 the current request boundary parameter is null 异常。

html中一般喜欢这样写，使用其他的样式来避免input[file]样式上的不足。（框架洁癖者请绕行）

```
...

<input type="text" ng-model="uploadData.type">

...

<a href class="file-upload" onclick="$('#files').trigger('click')">上传附件</a>

<input type="file" id="files" onchange="angular.element(this).scope().chooseFile(event)" style="display: none;" multiple>

...

```

咱们控制器中通过 event 来将文件拿到，再 push 到数组中，这样可以添加多个文件。

```

/**
 * 选择文件
 * /
$scope.chooseFile = function (event) {

	var files = event.target.files;

	angular.forEach(files, function (file) {
		
		$timeout(function () {
		
			$scope.uploadData.file.push(file);
			
		})
		
	});
	
};

/**
 * 删除文件
 * /
$scope.deleteFile = function (item) {

	var index = $scope.uploadData.file.indexOf(item);
	
	$scope.uploadData.file.splice(index, 1);

};

/**
 * 上传
 * /
$scope.upload = function () {

	/**
	 * httpServer 封装在服务中
	 * postUpload 执行 http_form_file_data 方法，并将 data 传过去
	 * /
	httpServer
		.postUpload($scope.uploadData)
		.then(function (result) {
		
			...

		})

};
                    
```

效果如下

![](http://omu1mo64e.bkt.clouddn.com/2017-4-3-01.png)

![](http://omu1mo64e.bkt.clouddn.com/2017-4-3-02.png)

##### 2.angular-file-upload

我们使用了很多的 angular-file-upload 来处理之前的上传，非常的好用，唯一麻烦的就是需要写很多的回调函数。详细使用参考 [angular-file-upload](https://github.com/nervgh/angular-file-upload)

##### 3.form表单

使用表单是一个比较通用并且简单的方法，这里不详细说明。

```
<from name="upload" action="url" method="post" enctype="multipart/form-data">
    <input type="text" name="style">
    <input type="file" name="file">
    <input type="submit" value="提交">
</from>
```


其他问题请联系作者：1742