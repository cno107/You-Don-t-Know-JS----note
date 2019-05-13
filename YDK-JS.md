# types & grammar

## ch1 --typeof

+ Typeof用来查看基本类型的 undefined boolean number string object symbol

```javascript
typeof null === "object"           //true      历史残留bug
typeof [1,2,3] === "object"        //true       
typeof function(){} === "object"   //true     "callable object"
//fun的length为arguments的个数
```

+ typeof    return的是字符串结果
+ 如何判断 arary类型   Object.prototype.toString.call( array  )      

```javascript
//首先 注意Object.prototype.toString 和 Object.toString() 不一样
let arrary = [1,2];
console.log(Object.prototype.toString.call(arrary))  //[object Array]
console.log(Object.prototype.toString.call(arrary)..slice(8,-1))  //Arrary
```

+ undefined   VS  "undeclared"

+ typeof可以用来判断作用域内 某个变量是否已被声明  可以减少thr error

  ```javascript
  let XXX = () => console.log('i am out XXX');
  
  let ch1 = () => {
      let helper =
          (typeof XXX !== "undefined") ?                    //有就用   没有自己建
          XXX : function () {
                return console.log('i am XXX');
              }
      helper();
  }
  
  ch1();    //i am out XXX
  ```

  简写为

  ```javascript
  let XXX = () => console.log('i am out XXX');
  
  let ch1 = (XXX) => {
      let helper = XXX || function(){console.log('???')}    //   ||
      helper();
  }
  
  ch1(XXX);
  ```

  

   



