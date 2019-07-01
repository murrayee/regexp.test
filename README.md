#### 数字

```js
// 连续3个数字
const p1 = /\d{3}/g;

// 连续两个相同数字
const p2 = /(\d)\1/g;

// 连续三个相同数字 相同
const p3 = /(\d)\1{2}/g;

// 连续4个或以上数字 相同
const p4 = /(\d)\1{3,}/g;

//正整数
const p5 = /^[1-9]\d*$/g; // /^[1-9]+$/g

//负整数
const p6 = /^-[1-9]\d*$/g; // /^-[1-9]+$/g

//整数
const p7 = /^[0-9]\d*$/g;

// 正浮点数
const p8 = /^[1-9]\d*\.\d*|0\.\d*[1-9]\d*$/;

//负浮点数
const p9 = /^-([1-9]\d*\.\d*|0\.\d*[1-9]\d*)$/g;

//浮点数
const p10 = /^-?([1-9]\d*\.\d*|0\.\d*[1-9]\d*|0?\.0+|0)$/g;

//中文字符
const p11 = /[\u4e00 - \u9fa5]/g;

//双字节中文字符
const p12 = /[ ^ \x00 - \xff]/;
```

#### `^` 和 `$` 的使用

```js
//假如我把 正浮点数 的正则写成这样 ：(0.\d+)|(\d+.\d+) ，现在开始匹配

//匹配一个字符串中的 正浮点数
const pattern = /(0.\d+)|(\d+.\d+)/;
console.log(pattern.test("0")); // false
console.log(pattern.test("0.5")); // true
console.log(pattern.test("a0.5")); // true
console.log(pattern.test("a0.5s")); // true
console.log(pattern.test("a0.a5s")); // false

//匹配以 `正浮点数` 开头或结尾 的字符串
const pattern = /^(0.\d+)|(\d+.\d+)$/;
console.log(pattern.test("0.5")); // true
console.log(pattern.test("a0.5")); // true
console.log(pattern.test("a0.5s")); // false
console.log(pattern.test("a0.a5s")); // false

//只匹配 正浮点数
const pattern = /^(0.\d+)$|^(\d+.\d+)$/;
//或      /^((0.\d+)|(\d+.\d+))$/
console.log(pattern.test("0.5")); // true
console.log(pattern.test("a0.5")); // false
console.log(pattern.test("a0.5s")); // false
console.log(pattern.test("a0.a5s")); // false
```

### 格式化日期

```js
//只匹配 日期格式：年-月-日
const pattern7 = /^\d{4}-(1[0-2]|0?[1-9])-(0?[1-9]|[12]\d|3[01])$/;
console.log(pattern7.test("ad2016-08-20ad")); // false
console.log(pattern7.test("2016-08-20")); // true
console.log(pattern7.test("2016-8-20")); // true
console.log(pattern7.test("16-08-20")); // false
console.log(pattern7.test("2016/08/20")); // false
//若去掉^和$
const pattern7 = /\d{4}-(1[0-2]|0?[1-9])-(0?[1-9]|[12]\d|3[01])/;
console.log(pattern7.test("ad2016-08-20ad")); // true

//只匹配 日期格式：年-月-日 或 年.月.日 或 年/月/日
const pattern7 = /^\d{4}(\/|\-|.)(0?[1-9]|1[0-2])\1(0?[1-9]|[12]\d|3[0-1])$/;
console.log(pattern7.test("ad2016-08-20ad")); // false
console.log(pattern7.test("2016-08-20")); // true
console.log(pattern7.test("2016/08/20")); // true
console.log(pattern7.test("2016.8.20")); // true
console.log(pattern7.test("2016-08-9")); // true
console.log(pattern7.test("2016/18/20")); // false
```

#### 时间

```js
//只匹配  时间格式：小时:分钟, 24小时制
const pattern8 = /^((0?|1)\d|2[0-3]):([0-5]\d)$/;
console.log(pattern8.test("13:45")); // true
console.log(pattern8.test("3:45")); // true
console.log(pattern8.test("13点45")); // false
```

#### 身份证号

```js
//只匹配 中国大陆身份证号，15位或18位
const pattern9 = /^\d{15}|\d{17}[\d|X]$/;
//或   /^\d{15}(\d{2}[0-9X])?$/
console.log(pattern9.test("15020416803082111X")); //true
console.log(pattern9.test("422322199901090033")); // true
console.log(pattern9.test("asdfasdfasfasdf123")); // false
```

#### 其它

```js
//只匹配 用户名
const p13 = /^[A-Za-z0-9_\/-\u4e00-\u9fa5]+$/;

//只匹配 长度为8-10的用户密码（以字母开头、数字、下划线）
const p14 = /^[A-z]\w{7,9}$/;

//只匹配 QQ号
const p15 = /^[1-9](\d{5,11})$/;

//只匹配 手机（国内）
const p16 = /^0?(13|14|15|17|18|19)[0-9]{9}$/;

// 1、合并：
// 0?[0-9]|1[0-9]可以合并为(0?|1)[0-9]
// \d{4}|\d{2} 不能合并为 \d({2}|{4}); //因为{N}代表次数

// 2、化简：
// [0-9] 化简写为 \d
// [A-Za-z0-9] 化简写为 [A-z0-9]

// 3、. 是 \w 和 \s效果的累加
```

#### 练习题

- 匹配字符串中所有的 HTML（1）标签头部 或 尾部 （2）标签头部（3）完整标签

```js
const str = 'ada<option value="hh">0</option>54<div id="as">adda</div>ad';
const result = str.match(/<.*>/g);
console.log(result); //["<option value="hh">0</option>54<div id="as">adda</div>"]

//（1）匹配 标签头部 或 尾部
const result = str.match(/<.*?>/g);
console.log(result); //["<option value="hh">", "</option>", "<div id="as">", "</div>"]

//（2）匹配 标签头部
const result2 = str.match(/<[A-z].*?>/g);
console.log(result2); // ["<option value="hh">", "<div id="as">"]

//（3）匹配 完整标签
const result3 = str.match(/<[A-z].*?>.*?<\/.*?>/g);
console.log(result3); // ["<option value="hh">0</option>", "<div id="as">adda</div>"]
```

- 写出正则表达式， 从一个字符串中提取所有链接地址。 比如下面字符串中

```js
const str =
  'IT面试题博客中包含很多<a href="http://hi.baidu.com/mianshiti/blog/category/微软面试题">微软面试题</a>';
const exg = /<a(?: [^>]*)+href="(.*)"(?: [^>]*)*>/g;
console.log(exg.exec(str)[1]);
//http://hi.baidu.com/mianshiti/blog/category/微软面试题
```

- 如何获取一个字符串中的数字字符，并按数组形式输出，如 ‘dgfhfgh254bhku289fgdhdy675gfh’ ，输出[254,289,675]

```js
const str = "dgfhfgh254bhku289fgdhdy675gfh";
console.log(str.match(/\d+/g)); //["254", "289", "675"]
```

- 敏感词过滤,比如：“我草你妈哈哈背景天胡景涛哪肉涯剪短发欲望”,过滤：‘草肉欲胡景涛’

```js
const str = "我草你妈哈哈背景天胡景涛哪肉涯剪短发欲望";
const result = str.replace(/草|肉|欲|胡|景|涛/g, "*");
console.log(result); //我*你妈哈哈背*天***哪*涯剪短发*望
```

- 判断是否符合 USD 格式:

```js
const pattern7 = /^\$\d{1,3}(,\d{3})*(\.\d{2})$/;
console.log(pattern7.test("$1,023,032.03")); // true
console.log(pattern7.test("$2.03")); // true
console.log(pattern7.test("$3,432,12.12")); // false
console.log(pattern7.test("$34,344.3")); // false
console.log(pattern7.test("da$2.03")); // false
```

- 给定字符串 str，检查其是否以元音字母结尾。
  元音字母包括 a，e，i，o，u，以及对应的大写；若包含则返回 true，否则返回 false

```js
function endsWithVowel(str) {
  return /[a,e,i,o,u]$/i.test(str);
}
console.log(endsWithVowel("gorilla")); //true
console.log(endsWithVowel("gorillE")); //true
console.log(endsWithVowel("gorillx")); //false
```

- 驼峰式字符串 borderLeftColor 和 连字符式字符串 border-left-color 相互转换

```js
const str = "borderLeftColor";
const str2 = "border-left-color";

///把str换成  连字符式
console.log(str.replace(/[A-Z]/g, item => "-" + item.toLowerCase())); //border-left-color
//把str换成  驼峰式
console.log(str2.replace(/-([a-z])/g, (item, $1) => $1.toUpperCase())); //borderLeftColor
```

- 对人口数字的格式化处理，三位数字用一个’,’(逗号)隔开

```js
function numberWithCommas(x) {
  //对右侧人口数字的格式化处理，三位数字用一个','(逗号)隔开
  return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
}
console.log(numberWithCommas(12345678)); //12,345,678
```

- 去掉 http 协议的 jpg 文件的协议头

```js
const imgs = [
  "http://img.host.com/images/fds.jpg",
  "https://img.host.com/images/fjlj.jpg",
  "http://img.host.com/images/djalsdf.png",
  "https://img.host.com/images/adsjfl.png",
  "http://img.host.com/image/jasdlf.jpg"
];
const result = imgs.map(img => {
  return img.replace(/http:(\/\/.+\.jpg)/, (item, $1) => {
    return $1;
  });
});
console.log(result);

// ["//img.host.com/images/fds.jpg",
//  "https://img.host.com/images/fjlj.jpg",
//	"http://img.host.com/images/djalsdf.png",
//	"https://img.host.com/images/adsjfl.png",
//	"//img.host.com/image/jasdlf.jpg"]
```

- 找出数组中的表示日期的时间字符串，并修改格式为‘月-日-年’

```js
const times = [
  "2006/02/03",
  "test/07/sd",
  "2016/05/10",
  "1998-03-07",
  "12345/23/45678",
  "1234/23/56789",
  "12345/23/45"
];
const result = times.map(time => {
  return time.replace(
    /^(\d{4})[/-](\d{2})[/-](\d{2})$/,
    (match, $1, $2, $3) => {
      return $1 - $2 - $3;
    }
  );
});
console.log(result);

//[ '02-03-2006',
// 'test/07/sd',
// '05-10-2016',
// '03-07-1998',
// '12345/23/45678',
// '1234/23/56789',
// '12345/23/45' ]
```

- 获取 url 中的参数

```js
//    获取 url 参数
function getUrlParam(sUrl, sKey) {
  const arr = {};
  sUrl.replace(/\??(\w+)=(\w+)&?/g, function(match, p1, p2) {
    //console.log(match,p1,p2);
    if (!arr[p1]) {
      arr[p1] = p2;
    } else {
      const p = arr[p1];
      arr[p1] = [].concat(p, p2);
    }
  });
  if (!sKey) return arr;
  else {
    for (const ele in arr) {
      if (ele == sKey) {
        return arr[ele];
      }
    }
    return "";
  }
}
```

- 让字符串制定部分变色
  让页面中这段字符串 “我爱你哈哈爱你” 中的”爱“字全变为红色。

```js
<div id="as">我爱你哈哈爱你</div>;

const oDiv = document.getElementById("as");
const str = oDiv.innerHTML;
const newStr = str.replace(
  /爱/g,
  m => "<span style='color:red'>" + m + "</span>"
);
oDiv.innerHTML = newStr;
```
