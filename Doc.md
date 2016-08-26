# baffle.js 中文文档

`baffle.js`是一个极简的(~1.8kb)用于DOM元素文本乱码模糊再恢复JavaScript库

> Github: [baffle.js](https://github.com/camwiegert/baffle)
> 下载: [最新发布的版本](https://raw.githubusercontent.com/camwiegert/baffle/master/dist/baffle.min.js)
> npm: [npm/baffle](https://npmjs.com/package/baffle)

```javascript
// 在任意元素上进行乱码模糊.
let b = baffle('.someSelector').start();
// 同样也适用于其他某些异步方法.
someAsyncFunction(result => {
    // 用异步获得的文本替换当前文本, 并在1500ms内恢复正常文字.
    b.text(currentText => result.text).reveal(1500);
});
```

## 获取baffle.js

你可以[下载最新发布的版本](https://raw.githubusercontent.com/camwiegert/baffle/master/dist/baffle.min.js)并且在包含引入到你的网页中`window.baffle`, 或者直接通过[NPM](https://www.npmjs.com/package/baffle)安装.

```bash
$ npm install --save baffle
```

## 基本用法

在`baffle`安装好后, 只需简单的调用 `baffle()` 并传入参数来实例化一个 `baffle` 对象. 参数可以是是以`CSS`选择器, 单一节点或者节点列表(`NodeList`). 你也可以额外传入一个 `options` 对象.

`baffle`的效果是作用于 `node.textContent` 上的, 所以这个效果也会影响到其子元素. 最好的办法就是在没有子结点的元素上使用`baffle`.

```javascript
// b 是一个 baffle 实例
// 使用CSS选择器
let b = baffle('.headline');

// 使用单一节点
let b = baffle(document.querySelector('.headline'));

// 使用节点列表
let b = baffle(document.querySelectorAll('a'));

// 传入options对象
let b = baffle('.headline', {
    characters: 'abcdefghijklmnopqrstuvwxyz',
    speed: 75
});
```

实例化`baffle`之后, 你可以通过使用 `start()` 方法来开始进行乱码模糊, 通过使用 `stop()` 方法来暂停, 或者通过 `reveal()` 方法来恢复到正常文本.


```javascript
// 开始进行乱码模糊
b.start();

// 暂停乱码模糊
b.stop();

// 立刻恢复正常文本
b.reveal();

// 在1000ms内恢复正常文本
b.reveal(1000);
```

同样地, 你可以在任何时间内调用 `text()` 来改变包含于 `baffle` 实例中的文本, 或者调用 `set()` 来改变 `options` 对象.


```javascript
/**
* text() 方法接收一个函数, 这个函数的唯一参数是
* 目前baffle实例中的文本, 并返回一个新的文本.
*/
b.text(currentText => currentText + '!');

// set() 方法接收一个 options 对象.
b.set({
    speed: 100,
    characters: '+-•~!=*'
});

// 只需在 options 对象中写入你想覆盖的属性
b.set({
    speed: 40
});
```


## 方法 (Methods)

`baffle`实例拥有6个可以链式调用的方法.

- `baffle.once()`

通过使用 `options.characters` 属性进行一次乱码处理.

- `baffle.start()`

在被`baffle`实例包裹的元素节点上进行乱码模糊, 更新速度由 `options.speed` (ms)来确定.

- `baffle.stop()`

暂停乱码效果. 注意, 这样并不会使你的元素的文字恢复正常, 只是暂停模糊变换而已. 要想文字恢复, 请使用 `reveal()` 方法.

- `baffle.reveal([duration], [delay])`

在持续时间 `duration` (ms)内(默认为0) 使得文本模糊褪去, 恢复正常文字. 可以通过传入的 `delay` (ms)规定延迟调用时间.

- `baffle.set([options])`
通过传入 `options` 对象来更新覆盖实例中的选项设置. 传入对象的属性数量任意, 而且你也可以在`baffle`运行时设置.

- `baffle.text(fn)` 
通过使用函数 `fn` 来更新你`baffle`实例中的每一个元素节点的文本. 该函数接受当前元素节点的文本作为唯一参数. 函数 `fn` 的返回值将作为新的文本来替换掉旧文本.

## 选项 (options)

你可以在`baffle`实例化或者使用 `set()` 方法设置`baffle`实例的时候传入一个 `options` 对象.
```javacript
// 进行实例化
baffle('.someSelector', {
    characters: 'supercalifragilisticexpialidocious',
    speed: 150
});

// 实例化之后的任何时机
baffle('.someSelector')
    .start()
    .set({
        characters: 'supercalifragilisticexpialidocious',
        speed: 150
    });
```

### 可用选项属性

- `options.characters`
baffle在用来进行乱码模糊使用的 "乱码" 字符. 它可以是一个字符串或者是一个元素是单个字符的数组.

默认值: `'AaBbCcDdEeFfGgHhIiJjKkLlMmNnOoPpQqRrSsTtUuVvWwXxYyZz~!@#$%^&*()-+=[]{}|;:,./<>?'`

- `options.exclude`
baffle进行乱码模糊时, 会忽略该属性设置的特定字符. 它可以是一个元素是单个字符的数组.

默认值: `[' ']`

- `options.speed`

这是用来表示`baffle`乱码模糊化时的更新频率.

默认值: `50`


## 浏览器兼容性

- √ 所有现代浏览器
- √ IE9+

当你遇到任何问题时, 欢迎[提出问题到issues](https://github.com/camwiegert/baffle/issues)

许可协议: MIT
作者: [Cam Wiegert](http://camwiegert.com/)
灵感来源: [Oak](http://oak.is/)
Language: [English](https://camwiegert.github.io/baffle/)
