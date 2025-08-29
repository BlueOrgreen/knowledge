
## this

> 普通函数的 `this` → 调用时看谁调用的; 箭头函数的 `this` → 定义时就锁定外层的 `this`


```js
const obj = {
  name: 'Alice',
  normal() {
    console.log(this);
  },
  arrow: () => {
    console.log(this);
  }
};

obj.normal(); // this = obj
obj.arrow();  // this = ??? （这里是window/undefined）

```


##### 嵌套函数

```js
const person = {
  name: 'Bob',
  showFriends() {
    ['Tom', 'Jerry'].forEach(function(friend) {
      console.log(this.name, friend);
    });
  }
};

person.showFriends();
// ❌ this = window / undefined → Cannot read property 'name'
```

why? => `forEach 里的普通 function → this 是全局`

用箭头函数修复

```js
const person = {
  name: 'Bob',
  showFriends() {
    ['Tom', 'Jerry'].forEach((friend) => {
      console.log(this.name, friend); // 箭头函数没有自己的 this, 它在定义时就继承外层 showFriends 里的 this → person
    });
  }
};

person.showFriends();
// ✅ this.name = 'Bob'
```

#### setTimeout 里的 this

```js
const obj = {
  name: 'Alice',
  sayHi() {
    setTimeout(function() {
        // setTimeout 里的 function → this 是 window
      console.log(this.name);
    }, 1000);
  }
};

obj.sayHi();
// ❌ undefined / window.name 
```

用箭头函数

```js
const obj = {
  name: 'Alice',
  sayHi() {
    setTimeout(() => {
      console.log(this.name);
    }, 1000);
  }
};

obj.sayHi();
// ✅ Alice
```