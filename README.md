TypeScript Add Declaration for Local ES-Module Compatible Js Files Demo
======================================================================

```
npm install
npm run demo
```

首先需要注意的是，`util.js`中虽然使用的是node的commonjs模块，但是它是与ES Module兼容的，
表现为它的`module.exports`是一个对象（而不是一个函数）。

对于这种情况，我们在import的时候，通常写法如下：

```
import * as util from './util'
```

注意需要使用`* as`。

直接写成`import util from './util'`是无法编译的，因为`./util`中没有`default`。

但是我们注意到，如果使用babel+js，那么这种情况下是可以写成`import util from './util'`的，
原因是babel会增加代码，在导入`./util`时，为其增加一个`default`属性，指向原模块。

在typescript中，实际上也可以做到这样，只需要我们在`tsconfig.json`中增加一个编译选项`esModuleInterop: true`，
那么typescript将使用与babel相似的处理方法，则我们可以写成：

- `import util from './util'`
- `import * as util from './util'`

两者效果相同。

注意：`esModuleInterop:true`是推荐一直开启为true的。
