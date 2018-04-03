# Nodejs 的 querystring模块

__querystring__ 从字面上理解就是查询字符串，
` 一般就是对http请求所带的数据进行解析 `

__querystring__ 模块只提供四个方法：
* querystring.parse
* querystring.stringify
* querystring.escape
* querystring.unescape

## 首先当然是把querystring模块引入了
```javascript
const querystring = require('querystring');
```
### 1. querystring.parse(str,separator,eq,options)

parse这个方法是将一个字符串反序列化成一个对象的
	参数：
* str 是指需要反序列化的字符串
*  separator(可省略) 指用于分割str，默认值为` & `
*  eq(可省略) 指用于划分键和值的字符或字符串，默认值为` = `
*  options(可省略) 该参数是一个对象，里面可设置maxkeys和decodeURIComponent这两个属性	：
		* maxKeys传入一个number类型，指定解析键值对的最大值，默认值是1000，如果设置为0，则取消解析的数量限制
		* decodeURIComponent 传入一个function，用于对含有%的字符串进行解码，默认值为`  querystring.unescape `

```
const str = 'name=Lokep&sex=male&sex=female';
const str_# = 'name=Lokep#sex=male#sex=female''
querystring.parse(str);
  /*
  return:{
    name:'Lokep',
    sex:['male','female']  
  }
  **/
  querystring.parse(str_#,'#',null,{maxKeys:2});
  /*
  return:{
    name:'Lokep',
    sex:'male'
  }
  **/
```

### 2. querystring.stringify
stringify这个方法是将一个对象序列化成一个字符串，与querystring.parse相对。
参数：
* obj指需要序列化的对象
* separator（可省）用于连接键值对的字符或字符串，默认值为"&";
* eq（可省）用于连接键和值的字符或字符串，默认值为"=";
* options（可省）传入一个对象，该对象可设置encodeURIComponent这个属性：
	* encodeURIComponent:值的类型为function，可以将一个不安全的url字符串转换成百分比的形式，默认值为querystring.escape()。

### 3.querystring.escape(str)
escape可使传入的字符串进行编码

### 4.querystring.unescape(str)
unescape方法可将含有%的字符串进行解码
