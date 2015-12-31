title: Node.js文件系统、路径的操作学习笔记
date: 2015-12-23 10:49:42
tags:
  - node.js
  - file
  - path
categories:
  - node
---

将Node.js的文件系统、文件流及路径操作API详细的学习了一下，代码都是测试过的，也许很简单，
但为了打好基础，还是要有点一丝不苟的精神，从中我也更深入理解异步回调事件机制，希望对你有用……

>公共引用

```
var fs = require('fs')
 ,path = require('path');
```


## 读取文件 readFile

readFile(filename,[options],callback);

* filename, 必选参数，文件名
* [options],可选参数，可指定flag（文件操作选项，如r+ 读写；w+ 读写，文件不存在则创建）及encoding属性
* callback 读取文件后的回调函数，参数默认第一个err,第二个data 数据


 
 ```js  
fs.readFile('/etc/passwd', function (err, data) {
  if (err) throw err;
  console.log(data);
});

```


## 写文件 writeFile

fs.writeFile(filename,data,[options],callback);
var w_data = '这是一段通过fs.writeFile函数写入的内容；\r\n';
var w_data = new Buffer(w_data);

* filename, 必选参数，文件名
* data, 写入的数据，可以字符或一个Buffer对象
* [options],flag,mode(权限),encoding
* callback 读取文件后的回调函数，参数默认第一个err,第二个data 数据

 
 ```js
fs.writeFile('message.txt', 'Hello Node.js', function (err) {
  if (err) throw err;
  console.log('It\'s saved!');
})
 ```
 
 ## 以追加方式写文件 appendFile
 
 fs.appendFile(filename,data,[options],callback);
 
 ```js
 fs.appendFile('message.txt', 'data to append', function (err) {
  if (err) throw err;
  console.log('The "data to append" was appended to file!');
});
 ```
 
 or
 
 ```js
 fs.appendFile('message.txt', 'data to append', 'utf8', callback);
 ```
 
 ## 打开文件 open
 
fs.open(filename, flags, [mode], callback);

 * filename, 必选参数，文件名
 * flags, 操作标识，如"r",读方式打开
 * [mode],权限，如777，表示任何用户读写可执行
 * callback 打开文件后回调函数，参数默认第一个err,第二个fd为一个整数，表示打开文件返回的文件描述符，window中又称文件句柄
 
```js
fs.open(__dirname + '/test.txt', 'r', '0666', function (err, fd) {
    console.log(fd);
});
```

## 读文件，读取打开的文件内容到缓冲区 read

fs.read(fd, buffer, offset, length, position, callback);

 * fd, 使用fs.open打开成功后返回的文件描述符
 * buffer, 一个Buffer对象，v8引擎分配的一段内存
 * offset, 整数，向缓存区中写入时的初始位置，以字节为单位
 * length, 整数，读取文件的长度
 * position, 整数，读取文件初始位置；文件大小以字节为单位
 * callback(err, bytesRead, buffer), 读取执行完成后回调函数，bytesRead实际读取字节数，被读取的缓存区对象
 
 ```js
 fs.open(__dirname + '/test.txt', 'r', function (err, fd) {
	if(err) {
		console.error(err);
		return;
	} else {
		var buffer = new Buffer(255);
		console.log(buffer.length);
		//每一个汉字utf8编码是3个字节，英文是1个字节
		fs.read(fd, buffer, 0, 9, 3, function (err, bytesRead, buffer) {
		if(err) {
			throw err;
			} else {
			console.log(bytesRead);
			console.log(buffer.slice(0, bytesRead).toString());
			//读取完后，再使用fd读取时，基点是基于上次读取位置计算;
			fs.read(fd, buffer, 0, 9, null, function (err, bytesRead, buffer) {
				console.log(bytesRead);
				console.log(buffer.slice(0, bytesRead).toString());
				});

			}

		});

	}

});
 ```
 
 ## 写文件，将缓冲区内数据写入使用fs.open打开的文件
 
fs.write(fd, buffer, offset, length, position, callback);

 * fd, 使用fs.open打开成功后返回的文件描述符
 * buffer, 一个Buffer对象，v8引擎分配的一段内存
 * offset, 整数，从缓存区中读取时的初始位置，以字节为单位
 * length, 整数，从缓存区中读取数据的字节数
 * position, 整数，写入文件初始位置；
 * callback(err, written, buffer), 写入操作执行完成后回调函数，written实际写入字节数，buffer被读取的缓存区对象
 
 ```js
fs.open(__dirname + '/test.txt', 'a', function (err, fd) {
	if(err) {
		console.error(err);
		return;
	} else {
		var buffer = new Buffer('写入文件数据内容');
		//写入'入文件'三个字
		fs.write(fd, buffer, 3, 9, 12, function (err, written, buffer) {
			if(err) {
				console.log('写入文件失败');
				console.error(err);
				return;
			} else {
				console.log(buffer.toString());
				fs.write(fd, buffer, 12, 9, null, function (err, written, buffer) {
					console.log(buffer.toString());
				})
			}
		});
	}
});
 ```
 
 ## 刷新缓存区 fsync
 
使用fs.write写入文件时，操作系统是将数据读到内存，再把数据写入到文件中，
当数据读完时并不代表数据已经写完，因为有一部分还可能在内在缓冲区内。

因此可以使用fs.fsync方法将内存中数据写入文件；--刷新内存缓冲区；

fs.fsync(fd, [callback])

 * fd, 使用fs.open打开成功后返回的文件描述符
 * [callback(err, written, buffer)], 写入操作执行完成后回调函数，written实际写入字节数，buffer被读取的缓存区对象

```js
fs.open(__dirname + '/test.txt', 'a', function (err, fd) {
	if(err)
		throw err;
	var buffer = new Buffer('我爱nodejs编程');
	
	fs.write(fd, buffer, 0, 9, 0, function (err, written, buffer) {
		console.log(written.toString());
		fs.write(fd, buffer, 9, buffer.length - 9, null, function (err, written) {
			console.log(written.toString());
			fs.fsync(fd);
			fs.close(fd);
		})
	});
});
```

## 创建目录 mkdir

使用fs.mkdir创建目录

fs.mkdir(path, [mode], callback);

 * path, 被创建目录的完整路径及目录名；
 * [mode], 目录权限，默认0777
 * [callback(err)], 创建完目录回调函数,err错误对象

```js
fs.mkdir(__dirname + '/fsDir', function (err) {
	if(err)
		throw err;	
	console.log('创建目录成功')
})
```

## 读取目录 readdir

使用fs.readdir读取目录，重点其回调函数中files对象

fs.readdir(path, callback);

 * path, 要读取目录的完整路径及目录名；
 * [callback(err, files)], 读完目录回调函数；err错误对象，files数组，存放读取到的目录中的所有文件名

```js
fs.readdir(__dirname + '/fsDir/', function (err, files) {
	if(err) {
		console.error(err);
		return;
	} else {
		files.forEach(function (file) {
			var filePath = path.normalize(__dirname + '/fsDir/' + file);
			fs.stat(filePath, function (err, stat) {
				if(stat.isFile()) {
					console.log(filePath + ' is: ' + 'file');
				}
				if(stat.isDirectory()) {
					console.log(filePath + ' is: ' + 'dir');
				}
			});
		});
		for (var i = 0; i < files.length; i++) {
			//使用闭包无法保证读取文件的顺序与数组中保存的致
			(function () {
				var filePath = path.normalize(__dirname + '/fsDir/' + files[i]);
				fs.stat(filePath, function (err, stat) {
					if(stat.isFile()) {
						console.log(filePath + ' is: ' + 'file');
					}
					if(stat.isDirectory()) {
						console.log(filePath + ' is: ' + 'dir');
					}
				});
			})();
		}
	}
});
```


## 查看文件与目录的信息 

fs.stat(path, callback);

fs.lstat(path, callback); //查看符号链接文件

 * path, 要查看目录/文件的完整路径及名；
 * [callback(err, stats)], 操作完成回调函数；err错误对象，stat fs.Stat一个对象实例，
 提供如:isFile, isDirectory,isBlockDevice等方法及size,ctime,mtime等属性

//实例，查看fs.readdir


## 查看文件与目录的是否存在 exists

fs.exists(path, callback);

 * path, 要查看目录/文件的完整路径及名；
 * [callback(exists)], 操作完成回调函数；exists true存在，false表示不存在

```js
fs.exists(__dirname + '/te', function (exists) {
	var retTxt = exists ? retTxt = '文件存在' : '文件不存在';
	console.log(retTxt);
});
```

## 修改文件访问时间与修改时间 utimes

fs.utimes(path, atime, mtime, callback);

 * path, 要查看目录/文件的完整路径及名；
 * atime, 新的访问时间
 * ctime, 新的修改时间
 * [callback(err)], 操作完成回调函数；err操作失败对象

```js
fs.utimes(__dirname + '/test.txt', new Date(), new Date(), function (err) {
	if(err) {
		console.error(err);
		return;
	}
	fs.stat(__dirname + '/test.txt', function (err, stat) {
		console.log('访问时间: ' + stat.atime.toString() + '; \n修改时间：' + stat.mtime);
		console.log(stat.mode);
	})
});
```

## 修改文件或目录的操作权限 chmod

fs.chmod(path, mode, callback);

 * path, 要查看目录/文件的完整路径及名；
 * mode, 指定权限，如：0666 8进制，权限：所有用户可读、写，
 * [callback(err)], 操作完成回调函数；err操作失败对象

```js
 fs.chmod(__dirname + '/fsDir', 0666, function (err) {
	if(err) {
		console.error(err);
		return;
	}
	console.log('修改权限成功')
});
```


## 移动/重命名文件或目录 rename

fs.rename(oldPath, newPath, callback);

 * oldPath, 原目录/文件的完整路径及名；
 * newPath, 新目录/文件的完整路径及名；如果新路径与原路径相同，而只文件名不同，则是重命名
 * [callback(err)], 操作完成回调函数；err操作失败对象

```js
fs.rename(__dirname + '/test', __dirname + '/fsDir', function (err) {
	if(err) {
		console.error(err);
		return;
	}
	console.log('重命名成功')
});
```

## 删除空目录 rmdir

fs.rmdir(path, callback);

 * path, 目录的完整路径及目录名；
 * [callback(err)], 操作完成回调函数；err操作失败对象

```js
fs.rmdir(__dirname + '/test', function (err) {
	fs.mkdir(__dirname + '/test', 0666, function (err) {
		console.log('创建test目录');
	});
	
	if(err) {
		console.log('删除空目录失败，可能原因：1、目录不存在，2、目录不为空')
		console.error(err);
		return;
	}

	console.log('删除空目录成功!');
})
```

## 监视文件 watchFile

对文件进行监视，并且在监视到文件被修改时执行处理 

fs.watchFile(filename, [options], listener);


 * filename, 完整路径及文件名；
 * [options], persistent true表示持续监视，不退出程序；interval 单位毫秒，表示每隔多少毫秒监视一次文件
 * listener, 文件发生变化时回调，有两个参数：curr为一个fs.Stat对象，被修改后文件，prev,一个fs.Stat对象，表示修改前对象
 
```js
fs.watchFile(__dirname + '/test.txt', {interval: 20}, function (curr, prev) {
	if(Date.parse(prev.ctime) == 0) {
		console.log('文件被创建!');
	} else if(Date.parse(curr.ctime) == 0) {
		console.log('文件被删除!')
	} else if(Date.parse(curr.mtime) != Date.parse(prev.mtime)) {
		console.log('文件有修改');
	}
});

fs.watchFile(__dirname + '/test.txt', function (curr, prev) {
	console.log('这是第二个watch,监视到文件有修改');
});
```