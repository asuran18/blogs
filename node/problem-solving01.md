#### problem 1
>Error: EXDEV, cross-device link not permitted (不允许跨分区重命名)

在使用node上传文件并进行重命名时报的错，代码如下：

	function upload(response, request) {
		var form = new formidable.IncomingForm();
		form.parse(request, function(error, fields, files) {
			//出错部分
			fs.renameSync(files.upload.path, '/tmp/test.png');
			
			...
		});
	}

在网上找到2种解决方法：

###### 方法1：

	function upload(response, request) {
		var form = new formidable.IncomingForm();
		form.uploadDir = 'tmp'; //添加一个临时路径
		form.parse(request, function(error, fields, files) {
			fs.renameSync(files.upload.path, '/tmp/test.png');

			...
		});
	}

###### 方法2：

	function upload(response, request) {
		var form = new formidable.IncomingForm();
		form.parse(request, function(error, fields, files) {
			var readStream = fs.createReadStream(files.upload.path);
			var writeStream = fs.createWriteStream('/tmp/test.png');
			readStream.pipe(writeStream);
			readStream.on('end',function() {
				fs.unlinkSync(files.upload.path);
			});

			...
		});
	}