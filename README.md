# Nodejs_study

### 今天想先看看FS模块

    Fs模块（文件系统）
    
> 从API上说呢，文件I/O是对标准的`POSIX`函数的简单封装，*POSIX 即 可移植性操作系统接口*
> 如同Nodejs的其他模块一样，它们都是通过`require('fs')`的方法来引入使用，
> 同样它也有异步和同步两种形式，最直观的区别就是——回调函数，

>异步方法的最后一个参数都是一个回调函数。 传给回调函数的参数取决于具体方法，但回调函数的第一个参数都会保留给异常。 如果操作成功完成，则第一个参数会是 null 或 undefined。
>当使用同步方法时，任何异常都会被立即抛出。 可以使用 try/catch 来处理异常，或让异常向上冒泡。
 
    __最基础的几种就是同异步读写__
    
* fs.readFile/fs.readFileSync
* fs.writeFile/fs.writeFileSync
* fs.rename/fs.renameSync
* fs.mkdir/fs.mkdirSync

1. 读取文件readFile函数

  fs.readFile(filename,[options],callback);
  
 * filename, 必选参数，文件名
 * [options],可选参数，可指定flag（文件操作选项，如r+ 读写；w+ 读写，文件不存在则创建）及encoding属性
 * callback 读取文件后的回调函数，参数默认第一个err,第二个data 数据
 
 ```Nodejs
 
 //公共引用
 var fs = require('fs'),
 path = require('path');
 
 fs.readFile(__dirname + '/test.txt', {flag: 'r+', encoding: 'utf8'}, function (err, data) {
    if(err) {
     console.error(err);
     return;
    }
    console.log(data);
});
```

   
2. 写文件

  fs.writeFile(filename,data,[options],callback);
  
 * filename, 必选参数，文件名
 * data, 写入的数据，可以字符或一个Buffer对象
 * [options],flag,mode(权限),encoding
 * callback 读取文件后的回调函数，参数默认第一个err,第二个data 数据
  
  ```Nodejs
  var w_data = '这是一段通过fs.writeFile函数写入的内容；\r\n';
  var w_data = new Buffer(w_data);
  
  fs.writeFile(__dirname + '/test.txt', w_data, {flag: 'a'}, function (err) {
   if(err) {
    console.error(err);
    } else {
       console.log('写入成功');
    }
  });
```

3.创建目录

  fs.mkdir(path,[mode],callback);
  使用fs.mkdir(path,[mode],callback)创建目录，
  
  * path是需要创建的目录，
  * [mode]是目录的权限（默认是0777），
  * callback是回调函数。
  
  ```Nodejs
  var fs = require('fs'); // 引入fs模块  
  
  // 创建 newdir 目录  
  fs.mkdir('./newdir', function(err) {  
      if (err) {  
          throw err;  
      }  
      console.log('make dir success.');  
  });  
  
  ```
  
  4. 读取目录readdir
  
    使用方式与mkdir类似
    
    ```Nodejs
    var fs = require('fs'); // 引入fs模块  
  
    fs.readdir('./newdir', function(err, files) {  
        if (err) {  
            throw err;  
        }  
        // files是一个数组  
        // 每个元素是此目录下的文件或文件夹的名称  
        console.log(files);  
    }); 
    ```
    
   5. 面对流文件的写入
   
    使用以下方法创建一个Writable流：

    fs.createWriteStream(path,[options]);
   
 > 往一个文件中写入大量数据，最好的方法就是使用流，把文件作为一个Writable打开，就可以往里面写数据，
 > 或是使用pipe()方法，将一个Readable流链接到Writable上，这样就很容易写来自源Readable流（如HTTP请求）的数据了；
    
   * path：指定文件的路径，可以是相对或是绝对路径；
   * options：定义字符串编码以及打开文件时使用的模式和标志的encoding、mode、和flag属性
    
    ```Nodejs
    var fs = require('fs');
    var grains = ['wheat', 'rice', 'oats'];/**/
    var options = { encoding: 'utf8', flag: 'w' };
    var fileWriteStream = fs.createWriteStream("../data/grains.txt",  options);
    fileWriteStream.on("close", function(){
      console.log("File Closed.");
    });
    while (grains.length){
      var data = grains.pop() + " ";
      fileWriteStream.write(data);
      console.log("Wrote: %s", data);
    }
    fileWriteStream.end();
   ```
   
