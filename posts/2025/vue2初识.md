---
title: Vue2初始
tags: [vue2]
categories: [技术]
date: 2025-05-10
description: 关于Vue2的一些内容
articleGPT: 这是一篇初始化文章，旨在告诉用户一些使用说明和须知。
references:
  - title: vue2相关文章
    url: http://bopeng.top
cover: http://cdn.bopeng.top/blog/vue.webp
---

# 初识

## 1. 初识 Vue

1. 想让 Vue 工作，就必须创建一个 Vue 实例，且要传入一个配置对象;
2. root 容器里的代码依然符合 html 规范，只不过混入了一些特殊的 Vue 语法;
3. root 容器里的代码被称为【Vue 模板】;
4. Vue 实例和容器是一一对应的;
5. 真实开发中只有一个 Vue 实例,并且会配合着组件一起使用;
6. {{xxx}}中的 xxx 要写 js 表达式，且 xxx 可以自动读取到 data 中的所有属性;
7. 一旦 data 中的数据发生改变，那么页面中用到该数据的地方也会自动更新;注意区分:js 表达式和 js 代码(语句)
8. 表达式:一个表达式会产生一个值，可以放在任何一个需要值的地方:

   (1). a

   (2). a+b

   (3). demo(1)

   (4). x === y ? 'a' : 'b'

9. js 代码(语句)

   (1). if(){}

   (2). for(){}

html

```
<body>
  <!-- 准备好一个容器 -->
  <div id="root"><h1>Hello,{{name}}</h1></div>
  <script>
    Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
    new Vue({
      el: '#root', // el用于指定当前Vue示例为哪个容器服务,值通常为css选择器字符串
      data: {
        // data中用于存储数据 数据供el所指定的容器去使用,值我们暂时先写成一个对象
        name: '大西瓜',
      },
    })
  </script>
</body>
```

## 2. 模板语法

Vue 模板语法有 2 大类:

1.插值语法:

功能: 用于解析标签体内容。

写法: {{xxx}},xxx 是 js 表达式，且可以直接读取到 data 中的所有属性。

2.指令语法:

功能: 用于解析标签（包括:标签属性、标签体内容、绑定事件.....） 。

举例: v-bind:href="xxx"或简写为:href="xxx"，xxx 同样要写 js 表达式，且可以直接读取到 data 中的所有属性。

备注: Vue 中有很多的指令，且形式都是: v-????，此处我们只是拿 v-bind 举个例子。

html

```html
<body>
  <!-- 准备好一个容器 -->
  <div id="root">
    <h1>插值语法</h1>
    <h3>你好,{{name}}</h3>
    <hr />
    <h1>指令语法</h1>
    <a v-bind:href="school.url.toUpperCase()">点我去{{school.name}}</a>
    <a :href="school.url">点我去{{school.name}}</a>
  </div>
  <script>
    Vue.config.productionTip = false; //阻止 vue 在启动时生成生产提示。
    new Vue({
      el: "#root",
      data: {
        name: "大西瓜",
        school: {
          name: "尚硅谷",
          url: "http://www.atguigu.com",
        },
      },
    });
  </script>
</body>
```

![img](https://images.bddxg.top/blog/image_xpWQZFpUIu.webp)

## 3. 数据绑定

Vue 中有 2 种数据绑定的方式:

1. 单向绑定(v-bind):数据只能从 data 流向页面。
2. 双向绑定(v-model):数据不仅能从 data 流向页面，还可以从页面流向 data。

**备注:**

1. 双向绑定一般都应用在表单类元素上(如:input、 select 等)
2. v-model:value 可以简写为 v-model，因为 v-model 默认收集的就是 value 值。

vue

```html
<body>
    <!-- 准备好一个容器 -->
    <div id="root">
        <!-- 普通写法 -->
        <!-- 单向数据绑定: <input type="text" v-bind:value="name"><br/>
            双向数据绑定: <input type="text" v-model:value="name"> -->
                <!-- 简写 -->
                单向数据绑定: <input type="text" :value="name"><br/>
                双向数据绑定: <input type="text" v-model="name">
  <script>
    Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
    new Vue({
        el:'#root',
        data: {
            name:'尚硅谷123'
        }
    })
  </script>
</body>
```

## 4. el 与 data 的两种写法

data 与 el 的 2 种写法

1. el 有 2 种写法

   (1). new Vue 时候配置 el 属性。

   (2). 先创建 Vue 实例，随后再通过 vm. $mount( ' #root ')指定 el 的值。

2. data 有 2 种写法

   (1).对象式

   (2).函数式

   如何选择:目前哪种写法都可以，以后学习到组件时，data 必须使用函数式，否则会报错。

3.一个重要的原则:

由 Vue 管理的函数，一定不要写箭头函数，一旦写了箭头函数，this 就不再是 Vue 实例了。

el 的 2 种写法:

html

```html
<body>
  <!-- 准备好一个容器 -->
  <div id="root">
    <h1>你好,{{name}}</h1>
  </div>
  <script>
    Vue.config.productionTip = false; // 阻止 vue 在启动时生成生产提示。
    // el的两种写法
    const v = new Vue({
      // el: "#root",
      data: {
        name: "尚硅谷",
      },
    });
    v.$mount("#root"); // 第二种写法
  </script>
</body>
```

data 的 2 种写法:

html

```html
<body>
  <!-- 准备好一个容器 -->
  <div id="root">
    <h1>你好,{{name}}</h1>
  </div>
  <script>
    Vue.config.productionTip = false; // 阻止 vue 在启动时生成生产提示。
    // el的两种写法
    const v = new Vue({
      // el的第一种写法
      el: "#root",
      /* data: {
          name: "尚硅谷",
        }, */
      data() {
        console.log(this.el);
        return {
          name: "尚硅谷",
        };
      },
    });
    // v.$mount("#root") // el的第二种写法
  </script>
</body>
```

## 5. MVVM 模型

MVVM 模型

1. M:模型(Model) : data 中的数据
2. V:视图(View):模板代码
3. VM:视图模型(ViewModel): Vue 实例

观察发现:

1. data 中所有的属性,最后都出现在了 vm 身上。
2. vm 身上所有的属性及 Vue 原型上所有属性，在 Vue 模板中都可以直接使用。

## 6. 数据代理

### 6.1 回顾 Object.defineProperty 方法

html

```
<script>
  let number = 18
  let person = {
    name: '大西瓜',
  }
  Object.defineProperty(person, 'age', {
    // value: 18,
    // // 控制属性是否可以枚举,默认值为false
    // enumerable: true,
    // // 控制属性是否可以被修改,默认值是false
    // writable:true,
    // // 控制属性是否可以被删除,默认值是false
    // configurable: true,
    // 当有人读取person的age属性时,get()函数(getter)就会被调用,且返回值就是age的值
    get() {
      console.log('有人读取了age的值')
      return number
    },
    set(value) {
      console.log('有人修改了age的值,是', value)
      number = value
    },
  })
</script>
```

### 6.2 何为数据代理

html

```html
<body>
  <!-- 数据代理:通过一个对象代理对另一个对象中属性的操作  读/写 -->
  <script>
    let obj1 = { x: 100 };
    let obj2 = { y: 100 };
    Object.defineProperty(obj2, "x", {
      get() {
        return obj1;
      },
      set(value) {
        obj1.x = value;
      },
    });
  </script>
</body>
```

### 6.3 Vue 中的数据代理

1.Vue 中的数据代理:

通过 vm 对象来代理 data 对象中属性的操作（读/写)

2.Vue 中数据代理的好处:

更加方便的操作 data 中的数据

3.基本原理:

通过 object.defineProperty()把 data 对象中所有属性添加到 vm 上.为每一个添加到 vm 上的属性，都指定一个 getter/setter。

在 getter/setter 内部去操作（读/写)data 中对应的属性。

![img](https://images.bddxg.top/blog/image_TjQzqrWjfx.webp)

html

```html
<body>
  <!-- 准备好一个容器 -->
  <div id="root">
    <h2>学校名称:{{name}}</h2>
    <h2>学校地址:{{address}}</h2>
  </div>
  <script>
    //阻止 vue 在启动时生成生产提示。
    Vue.config.productionTip = false;
    const vm = new Vue({
      el: "#root",
      data: {
        name: "尚硅谷",
        address: "宏福科技园",
      },
    });
  </script>
</body>
```

## 7. 事件处理

### 7.1 事件的基本使用

事件的基本使用:

1. 使用 v-on :xxx 或@xxx 绑定事件,其中 xxx 是事件名;
2. 事件的回调需要配置在 methods 对象中，最终会在 vm 上;
3. methods 中配置的函数，不要用箭头函数!否则 this 就不是 vm 了;
4. methods 中配置的函数，都是被 Vue 所管理的函数，this 的指向是 vm 或组件实例对象;
5. @click="demo”和@click=""demo（$event)”效果一致，但后者可以传参;

html

```html
<body>
  <!-- 准备好一个容器 -->
  <div id="root">
    <h2>欢迎来到{{name}}学习</h2>
    <!-- 普通事件绑定写法 -->
    <!-- <button v-on:click="showInfo">点我提示信息</button> -->
    <!-- 简写 -->
    <button @click="showInfo1">点我提示信息1</button>
    <button @click="showInfo2($event,66)">点我提示信息2</button>
  </div>
  <script>
    //阻止 vue 在启动时生成生产提示。
    Vue.config.productionTip = false;
    const vm = new Vue({
      el: "#root",
      data: {
        name: "尚硅谷",
      },
      methods: {
        showInfo1(event) {
          console.log(this); // 此处是this是vm
          alert("同学你好!");
        },
        showInfo2(event, number) {
          console.log(number);
        },
      },
    });
  </script>
</body>
```

### 7.2 事件修饰符

Vue 中的事件修饰符:

1. prevent:阻止默认事件（常用）;
2. stop:阻止事件冒泡（常用）;
3. once:事件只触发一次（常用）;
4. capture:使用事件的捕获模式;
5. self:只有 event.target 是当前操作的元素是才触发事件;
6. passive:事件的默认行为立即执行，无需等待事件回调执行完毕;

html

```html
<body>
  <div id="root">
    <h2>欢迎来到{{name}}学习</h2>
    <!-- 阻止默认事件(常用) -->
    <a href="http://www.atguigu.com" @click.prevent="showInfo">点我提示信息</a>
    <!-- 阻止事件冒泡(常用) -->
    <div class="demo1" @click="showInfo">
      <!-- <button @click.stop="showInfo">点我提示信息(防冒泡)</button> -->
      <!-- 修饰符可以连续写 -->
      <a href="http://www.atguigu.com" @click.stop.prevent="showInfo">点我提示信息(防冒泡)</a>
    </div>
    <!-- 事件只触发一次(常用) -->
    <button @click.once="showInfo">点我提示信息(仅一次)</button>
    <!-- 事件捕获模式 -->
    <div class="box1" @click.capture="showMsg(1)">
      div1
      <div class="box2" @click="showMsg(2)">div2</div>
    </div>
    <!-- 只有event.target 是当前操作的元素时才触发事件 -->
    <div class="demo1" @click.self="showInfo">
      <button @click="showInfo">点我提示信息</button>
    </div>
    <!-- 事件的默认行为立即执行，无需等待事件回调执行完毕; -->
    <!-- 常用在移动端页面设计 属性:wheel -->
    <ul @scroll.passive="demo" class="list">
      <li>1</li>
      <li>2</li>
      <li>3</li>
      <li>4</li>
    </ul>
  </div>
  <script>
    // 阻止 vue 在启动时生成生产提示。
    Vue.config.productionTip = false;
    new Vue({
      el: "#root",
      data: {
        name: "尚硅谷",
      },
      methods: {
        showInfo(e) {
          // e.preventDefault()
          // alert("同学你好!")
          console.log(e.target);
        },
        showMsg(number) {
          console.log(number);
        },
        demo() {
          console.log("@");
        },
      },
    });
  </script>
</body>
```

### 7.3 键盘事件

1. Vue 中常用的按键别名:

- 回车=> enter
- 删除=> delete(捕获“删除”和“退格”键)退出=>esc
- 空格=> space
- 换行=> tab(特殊，必须配合 keydown 去使用)
- 上=> up
- 下=> down
- 左=> left
- 右=> right

1. Vue 未提供别名的按键，可以使用按键原始的 key 值去绑定，但注意要转为 kebab-case（短横线命名)
2. 系统修饰键（用法特殊）:ctrl、alt、shift、meta

   (1).配合 keyup 使用:按下修饰键的同时，再按下其他键，随后释放其他键，事件才被触发。

   (2).配合 keydown 使用:正常触发事件。

3. 也可以使用 keyCode 去指定具体的按键（不推荐)
4. Vue.config.keyCodes.自定义键名=键码，可以去定制按键别名

html

```html
<body>
  <div id="root">
    <input type="text" placeholder="按下回车提示输入" @keyup.enter="showInfo" />
    <!-- 组合键 -->
    <input type="text" placeholder="按下回车提示输入" @keyup.ctrl.y="showInfo" />
  </div>
  <script>
    //阻止 vue 在启动时生成生产提示。
    Vue.config.productionTip = false;
    new Vue({
      el: "#root",
      methods: {
        showInfo(e) {
          console.log(e.target.value);
        },
      },
    });
  </script>
</body>
```

## 8. 计算属性

计算属性:

1. 定义:要用的属性不存在,要通过已有属性计算得来。
2. 原理:底层借助了 objcet.defineproperty 方法提供的 getter 和 lsetter.
3. get 函数什么时候执行?

   (1).初次读取时会执行一次。

   (2).当依赖的数据发生改变时会被再次调用。

4. 优势:与 methods 实现相比，内部有缓存机制（复用），效率更高，调试方便。
5. 备注:

   (1).计算属性最终会出现在 vm 上，直接读取使用即可。

   (2).如果计算属性要被修改，那必须写 set 函数去响应修改，且 set 中要引起计算时依赖的数据发生改变。

### 8.1 插值语法实现

html

```html
<body>
  <div id="root">
    姓:
    <input type="text" v-model="fn" />
    <br />
    名:
    <input type="text" v-model="ln" />
    <br />
    全名:
    <span>{{fn}}-{{ln}}</span>
  </div>
  <script>
    //阻止 vue 在启动时生成生产提示。
    Vue.config.productionTip = false;
    new Vue({
      el: "#root",
      data: {
        fn: "张",
        ln: "三",
      },
    });
  </script>
</body>
```

23

### 8.2 methods 实现

html

```html
<body>
  <div id="root">
    姓:
    <input type="text" v-model="fn" />
    <br />
    名:
    <input type="text" v-model="ln" />
    <br />
    全名:
    <span>{{showInfo()}}</span>
  </div>
  <script>
    //阻止 vue 在启动时生成生产提示。
    Vue.config.productionTip = false;
    new Vue({
      el: "#root",
      data: {
        fn: "张",
        ln: "三",
      },
      methods: {
        showInfo() {
          return this.fn + "-" + this.ln;
        },
      },
    });
  </script>
</body>
```

### 8.3 计算属性实现

html

```html
<body>
  <div id="root">
    姓:
    <input type="text" v-model="fn" />
    <br />
    名:
    <input type="text" v-model="ln" />
    <br />
    全名:
    <span>{{fullname}}</span>
  </div>
  <script>
    //阻止 vue 在启动时生成生产提示。
    Vue.config.productionTip = false;
    const vm = new Vue({
      el: "#root",
      data: {
        fn: "张",
        ln: "三",
      },
      computed: {
        fullname: {
          //get有什么作用? 当有人读取fullName时，get就会被调用，且返回值就作为fullName的值
          //get什么时候调用?1.初次读取fullName时。2.所依赖的数据发生变化时。
          get() {
            // console.log(this) // 此处的this是vm
            return this.fn + "-" + this.ln;
          },
          // set什么时候被调用? 当fullname被修改时
          set(value) {
            let arr = value.split("-");
            this.fn = arr[0];
            this.ln = arr[1];
          },
        },
      },
    });
  </script>
</body>
```

### 8.4 计算属性简写

注意:仅能在计算属性只有 getter 的情况下才能简写

html

```html
<body>
  <div id="root">
    姓:
    <input type="text" v-model="fn" />
    <br />
    名:
    <input type="text" v-model="ln" />
    <br />
    全名:
    <span>{{fullName}}</span>
  </div>
  <script>
    //阻止 vue 在启动时生成生产提示。
    Vue.config.productionTip = false;
    const vm = new Vue({
      el: "#root",
      data: {
        fn: "张",
        ln: "三",
      },
      computed: {
        // 简写
        fullName() {
          console.log("get被调用了");
          return this.fn + "-" + this.ln;
        },
      },
    });
  </script>
</body>
```

## 9. 监视属性

### 9.1 天气案例

html

```html
<body>
  <!-- 准备好一个容器 -->
  <div id="root">
    <h2>今天天气很{{info}}</h2>
    <!-- 简单写法 -->
    <button @click="isHot=!isHot">切换天气</button>
    <!-- 普通写法 -->
    <!-- <button @click="changeWeather">切换天气</button> -->
  </div>
  <script>
    // 取消启动提示
    Vue.config.productionTip = false;
    new Vue({
      el: "#root",
      data: {
        isHot: true,
      },
      computed: {
        info() {
          return this.isHot ? "炎热" : "凉爽";
        },
      },
      methods: {
        changeWeather() {
          this.isHot = !this.isHot;
        },
      },
    });
  </script>
</body>
```

### 9.2 监视属性

监视属性 watch:

1. 当被监视的属性变化时,回调函数自动调用,进行相关操作
2. 监视的属性必须存在,才能进行监视!!
3. 监视的两种写法:

   (1).new Vue 时传入 watch 配置

   (2).通过 vm.$watch 监视

   html

   ```html
   <body>
     <!-- 准备好一个容器 -->
     <div id="root">
       <h2>今天天气很{{info}}</h2>
       <button @click="changeWeather">切换天气</button>
     </div>
     <script>
       // 取消启动提示
       Vue.config.productionTip = false;
       new Vue({
         el: "#root",
         data: {
           isHot: true,
         },
         computed: {
           info() {
             return this.isHot ? "炎热" : "凉爽";
           },
         },
         methods: {
           changeWeather() {
             this.isHot = !this.isHot;
           },
         },
         watch: {
           info: {
             immediate: true, // 初始化时调用一次handler
             // handler 什么时候调用,当info被修改时
             handler(newvalue, oldvalue) {
               console.log(`isHos的值被修改了,修改之前是 ${oldvalue},修改之后是 ${newvalue}`);
             },
           },
         },
       });
       // // 第二种监视方式
       // vm.$watch("info", {
       //   immediate: true,
       //   handler(newvalue, oldvalue) {
       //     console.log(
       //       `isHos的值被修改了,修改之前是 ${oldvalue},修改之后是 ${newvalue}`
       //     )
       //   },
       // })
     </script>
   </body>
   ```

### 9.3 深度监视

深度监视:

(1).vue 中的 watch 默认不监测对象内部值的改变（一层）。

(2).配置 deep:true 可以监测对象内部值改变（多层)。

备注:

(1).Vue 自身可以监测对象内部值的改变，但 vue 提供的 watch 默认不可以!

(2).使用 watch 时根据数据的具体结构,决定是否采用深度监视。

html

```html
<body>
  <!-- 准备好一个容器 -->
  <div id="root">
    <h3>a的值是:{{numbers.a}}</h3>
    <button @click="numbers.a++">点我让a++</button>
    <h3>b的值是:{{numbers.b}}</h3>
    <button @click="numbers.b++">点我让b++</button>
  </div>
  <script>
    // 取消启动提示
    Vue.config.productionTip = false;
    let vm = new Vue({
      el: "#root",
      data: {
        numbers: {
          a: 1,
          b: 2,
        },
      },
      watch: {
        "numbers.a": {
          handler() {
            console.log("a的值被改变了");
          },
        },
        numbers: {
          deep: true,
          handler() {
            console.log("number的值改变了");
          },
        },
      },
    });
  </script>
</body>
```

### 9.4 深度监视简写

html

```html
<body>
  <!-- 准备好一个容器 -->
  <div id="root">
    <h2>今天天气很{{info}}</h2>
    <button @click="changeWeather">切换天气</button>
  </div>
  <script>
    // 取消启动提示
    Vue.config.productionTip = false;
    let vm = new Vue({
      el: "#root",
      data: {
        isHot: true,
      },
      computed: {
        info() {
          return this.isHot ? "炎热" : "凉爽";
        },
      },
      methods: {
        changeWeather() {
          this.isHot = !this.isHot;
        },
      },
      watch: {
        // 正常写法
        // info: {
        //   immediate: true, // 初始化时调用一次handler
        //   // handler 什么时候调用,当info被修改时
        //   handler(newvalue, oldvalue) {
        //     console.log(
        //       `isHos的值被修改了,修改之前是 ${oldvalue},修改之后是 ${newvalue}`
        //     )
        //   },
        // },
        // 简写
        info(newvalue, oldvalue) {
          console.log(`isHos的值被修改了,修改之前是 ${oldvalue},修改之后是 ${newvalue}`);
        },
      },
    });
    // 正常写法
    // vm.$watch("info", {
    //   immediate: true,
    //   handler(newvalue, oldvalue) {
    //     console.log(
    //       `isHos的值被修改了,修改之前是 ${oldvalue},修改之后是 ${newvalue}`
    //     )
    //   },
    // })
    // 简写
    // vm.$watch("info", function (newvalue, oldvalue) {
    //   console.log(
    //     `isHos的值被修改了,修改之前是 ${oldvalue},修改之后是 ${newvalue}`
    //   )
    // })
  </script>
</body>
```

### 9.5 姓名案例 watch 实现

computed 和 Iwatch 之间的区别:

1. computed 能完成的功能,watch 都可以完成。
2. watch 能完成的功能，computed 不一定能完成，例如: watch 可以进行异步操作。

两个重要的小原则:

1. 所被 Vue 管理的函数，最好写成普通函数，这样 this 的指向才是 vm 或组件实例对象.
2. 所有不被 Vue 所管理的函数（定时器的回调函数、ajax 的回调函数等、Promise 的回调函数)，最好写成箭头函数,这样 this 的指向才是 vm 或组件实例对象。

html

```
<body>
  <div id="root">
    姓:
    <input type="text" v-model="fn" />
    <br />
    名:
    <input type="text" v-model="ln" />
    <br />
    全名:
    <span>{{fullName}}</span>
  </div>
  <script>
    //阻止 vue 在启动时生成生产提示。
    Vue.config.productionTip = false
    const vm = new Vue({
      el: '#root',
      data: {
        fn: '张',
        ln: '三',
        fullName: '张-三',
      },
      watch: {
        fn(val) {
          setTimeout(() => {
            this.fullName = val + '-' + this.ln
          }, 1000)
        },
        ln(val) {
          this.fullName = this.fn + '-' + val
        },
      },
    })
  </script>
</body>
```

## 10. 绑定样式

html

```html
<style>
    .basic {
        width: 300px;
        height: 100px;
        border: 1px solid rgb(33, 33, 33);
        text-align: center;
        line-height: 100px;
        user-select: none;
    }
    .normal {
        background-image: linear-gradient(to top, #fad0c4 0%, #ffd1ff 100%);
    }
    .sad {
        background-image: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    }
    .happy {
        background-image: linear-gradient(120deg, #89f7fe 0%, #66a6ff 100%);
    }
    .at1 {
        font-size: 2em;
        color: red;
        text-shadow: 0 0 0.2em #f87, 0 0 0.2em #f87;
    }
    .at2 {
        border-radius: 15px;
    }
    .at3 {
        background-image: linear-gradient(120deg, #d4fc79 0%, #96e6a1 100%);
    }
</style>
<title>绑定样式</title>
</head>
<body>
    <div id="root">
        <!-- 绑定class样式 字符串写法 适用于:样式的类名不确定,需要动态指定 -->
        <div class="basic" :class="mod" @click="changeMod">{{name}}</div>
        <br />
        <br />
        <!-- 绑定class样式 数组写法,适用于:要绑定的样式个数不确定,名字也不确定 -->
        <div class="basic" :class="classArr">大西瓜</div>
        <br />
        <br />
        <!-- 绑定class样式 对象写法 适用于:要绑定的样式个数确定,名字确定,但动态决定用不用 -->
        <div class="basic" :class="classObj">尚硅谷</div>
        <br />
        <br />
        <!-- 绑定style样式 对象写法 -->
        <div class="basic" :style="styleObj">绑定style样式</div>
        <br />
        <br />
        <!-- 绑定style样式 数组写法 -->
        <div class="basic" :style="styleArr">绑定style样式</div>
        <br />
        <br />
    </div>
    <script>
        // 关闭启动提示
        Vue.config.productionTip = false
        new Vue({
            el: "#root",
            data: {
                name: "尚硅谷",
                mod: "nomal",
                classArr: ["at1", "at2", "at3"],
                classObj: {
                    at1: true,
                    at2: true,
                },
                styleObj: {
                    color: "red",
                    fontSize: "30px",
                },
                styleObj2: {
                    backgroundColor: "orange",
                },
                styleArr: [
                    {
                        color: "red",
                        fontSize: "30px",
                    },
                    {
                        backgroundColor: "orange",
                    },
                ],
            },
            methods: {
                changeMod() {
                    const arr = ["happy", "sad", "normal"]
                    // 利用Math.random随机选择数组元素
                    this.mod = arr[Math.floor(Math.random() * 3)]
                },
            },
        })
    </script>
</body>
```
