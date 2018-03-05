# Nodejs_study

## today ,李哥flag，每天学习一些NodeJs

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
   
