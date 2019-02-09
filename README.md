TypeScript Add Declaratio for Local ES-Module Compatible Js Files Demo
======================================================================

```
npm install
npm run demo
```

首先需要注意的是，`util.js`中虽然使用的是node的commonjs模块，但是它是与ES Module兼容的，
表现为它的`module.exports`是一个对象（而不是一个函数）：

```
module.exports = {toUpper};
```

对于这种情况，我们可以如`util.d.ts`中所示，简单的给它增加类型说明：

```
export declare function toUpper(str: string): string
```

使用的时候也非常简单，就是正常的写法：

```
import * as util from './util';

console.log(`Hello, ${util.toUpper('typescript')}`);
```

它将被编译为：

```
Object.defineProperty(exports, "__esModule", { value: true });
const util = require("./util");
console.log(`Hello, ${util.toUpper('typescript')}`);
```

可以看到在导入和使用`./util`时，没有做什么特殊处理。

需要注意的是：

- 我们可以使用typescript的`esModuleInterop:true`来简化`import`的写法，去掉`* as`（见另一个demo）
- 如果`./util.js`是一个与es-module不兼容的模块，则当前代码无法编译，需要特别的处理。（见另一个demo）
