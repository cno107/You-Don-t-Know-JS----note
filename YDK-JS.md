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
## ch2 --arrary

### arrary

```javascript

let arr = [];
arr[0] =  'a';
arr[1] = 'b';
arr[3] = 'd';
delete  arr[1];   //一つを削除しても　配列長さも変わらない
console.log(arr.length);   //4
console.log(arr);          //[ 'a', <2 empty items>, 'd' ]
console.log(typeof arr[1]);  //undefined

arr[1]  = undefined;
console.log(arr);  //[ 'a', undefined, <1 empty item>, 'd' ]
console.log(arr[1] === arr[2]);   //true 但是又不一样 见ch3
```

+ let arr[1]  和 let arr[1] = undefined 不一样

+ arr[ “107”] 和 arr[107 ]  一样 但是最好别用
   - 如果只定义一个 arr['107'] 会自动转换为index 且长度变为108 前107全部为 empty
+ arr [ “a”] これでもいい、但是不可数, 也不算入length里
   - 调用时 arr.a  arr['a']都可以


```javascript
let brr = [];
brr['0'] = 'phb';
brr['age'] = '20';
console.log(brr);       //[ 'phb', age: '20' ]
console.log(brr.length);  //   1
console.log(brr.age === brr["age"]);  //true   说明可用
```

### Arrary-Likes

+ 例如 arguments    可以将其转换为数组
+ ```Array.prototype.slice.call(arguments)```
+ ```Array.from(arguments)```

```javascript
function  fun(){
    console.log(arguments);  //{ '0': 'a', '1': 'b', '2': 'c' }
    let arr = Array.prototype.slice.call(arguments);
    //能将具有length属性的对象转成数组
    let arrEs6 = Array.from(arguments);  //es6
    console.log(arr,arrEs6);//[ 'a', 'b', 'c' ]
}

fun('a','b','c');
```




