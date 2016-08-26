# baffle.js

一个用于DOM元素**文本乱码模糊再恢复**的极简JavaScript库

[camwiegert.github.io/baffle](https://camwiegert.github.io/baffle)

> <img src="https://camwiegert.github.io/baffle/assets/images/baffle.js.png" width="500" alt="baffle.js">


- 压缩约 ~1.8kb!  (｡・`ω´･)
- 没有任何依赖!  (ﾉ･ω･)ﾉﾞ
- 支持IE9+!  ヽ(•̀ω•́ )ゝ

```javascript
// 使用选择器选择元素并开始乱码模糊.
let b = baffle('.someSelector').start();

// 同样也适用于其他某些异步方法.
someAsyncFunction(result => {
    // 用异步获得的文本替换当前文本, 并在1500ms内恢复正常文字.
    b.text(text => result.text).reveal(1500);
});
```

---

## 起步

#### 步骤 0: 安装

[直接下载最新的发布的版本](https://raw.githubusercontent.com/camwiegert/baffle/master/dist/baffle.min.js) 或者使用`npm`包管理器安装.

```sh
npm install --save baffle
```

#### 步骤 1: 引入
如果你直接使用`HTML`标签直接引入代码, 那么你之后可以通过 `window.baffle` 来使用本库. 在模块化开发中, 你可以直接使用模块导入本库.

```javascript
// CommonJS 方式
let baffle = require('baffle');

// ES6 导入方式
import baffle from 'baffle';
```

#### 步骤 2: 初始化/实例化
你需要使用一些元素节点来初始化一个baffle实例. 你可以传入一个节点列表(`NodeList`), 一个节点(`Node`) 或者 是一个选择器.

```javascript
// 传入选择器.
let b = baffle('.baffle');

// 传入节点列表(NodeList)
let b = baffle(document.querySelectorAll('.baffle'));

// 传入单个节点(Node)
let b = baffle(document.querySelector('.baffle'));
```

#### 步骤 3: 尽情使用
对于一个`baffle`实例, 有多种方法可以调用. 通常, 我们会调用 `b.start()` 开始进行乱码模糊, 然后调用 `b.reveal()` 来恢复.

```javascript
// 开始进行乱码模糊...
b.start();

// 或者暂停乱码模糊...
b.stop();

// 进行一次乱码渲染...
b.once();

// 在初始化之后, 你可以设置一些选项...
b.set({...options});

// 或者在任何时候改变文本...
b.text(text => 'Hi Mom!');

// 最终, 你会使文本恢复到正常...
b.reveal(1000);

// 除此之外, 这些方法都可以链式调用...
b.start()
    .set({ speed: 100 })
    .text(text => 'Hi dad!')
    .reveal(1000);
```

## 选项 (options)
在初始化的时候, 你可以传入`options`对象来配置一些设置. 同样, 你也可以调用 `baffle.set()`来进行设置.

```javascript
// 初始化时...
baffle('.baffle', {
    characters: '+#-•=~*',
    speed: 75
});

// 任何时机调用set()
b.set({
    characters: '¯\_(ツ)_/¯',
    speed: 25
});
```

> ### `options.characters`
> 这个属性指的是`baffle`在用来进行乱码模糊使用的 "乱码" 字符. 它可以是一个字符串(`string`)或者是 一个元素是单个字符的数组(`an array of characters`).
>
> **默认值:** `'AaBbCcDdEeFfGgHhIiJjKkLlMmNnOoPpQqRrSsTtUuVvWwXxYyZz~!@#$%^&*()-+=[]{}|;:,./<>?'`

> ### `options.exclude`
> 这个属性指的是`baffle`进行乱码模糊时, 会忽略该属性设置的特定字符. 它可以是一个元素是单个字符的数组(`an array of characters`).
>
> **默认值:** `[' ']`

> ### `options.speed`
> 表示`baffle`乱码模糊化时的更新频率..
>
> **Default:** `50`

## 方法(methods)

`baffle`实例拥有6个可以链式调用的方法..

> ###`baffle.once()`
> 通过使用 `options.characters` 属性进行一次乱码处理.

> ###`baffle.start()`
> 在被`baffle`实例包裹的元素节点上进行乱码模糊, 更新速度由 `options.speed` (ms)来确定.

> ###`baffle.stop()`
> 暂停乱码效果. 注意, 这样并不会使你的元素的文字恢复正常, 只是暂停模糊变换而已. 要想文字恢复, 请使用 `reveal()` 方法.

> ###`baffle.reveal([duration], [delay])`
> 在持续时间 `duration` (ms)内(默认为0) 使得文本模糊褪去, 恢复正常文字. 可以通过传入的 `delay` (ms)规定延迟调用时间.

> ###`baffle.set([options])`
> 通过传入 options 对象来更新覆盖实例中的选项设置. 传入对象的属性数量任意, 而且你也可以在baffle运行时设置

> ###`baffle.text(fn)`
> 通过使用函数 `fn` 来更新你`baffle`实例中的每一个元素节点的文本. 该函数接受当前元素节点的文本作为唯一参数. 函数 `fn` 的返回值将作为新的文本来替换掉旧文本.

---

- **许可协议:** MIT
- **作者:** [Cam Wiegert](http://camwiegert.com)
- **灵感来源:** [Oak](http://oak.is/)
- **Language:** [English](https://github.com/camwiegert/baffle)
