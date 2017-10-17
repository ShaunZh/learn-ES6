##知识点
- ES6明确规定，如果区块中存在`let`和`const`命令，那么在该区块开始时就形成了**封闭作用域**，凡是 **在变量声明前就使用这些变量，就会报错**。
  总之，使用`let`声明的变量，只能在声明之后才能使用，这在语法上称为：**暂时性死区（temporal dead zone，简称TDZ）**
  例如：
  ```js
  if (true) {
    // TDZ开始
    temp = 'abc';       // ReferenceError
    console.log(temp);  // ReferenceError

    let temp ;          // temp声明，导致TDZ结束
    console.log(temp);  // undefined

    temp = 123;
    console.log(temp);
  }
  ```

- 使用`let`声明的变量，`typeof`不再是一个百分百安全的操作  
  ```js
    typeof x;           // ReferenceError
    let x;                

    typeof undeclared_variable  // "undefined"
    ```
    上面代码中，`let x`声明在使用`typeof x`之后，因此也会报错误；相反，对于一个没有定义的变量：`undeclared_variable`，反而不会报错，因为该变量被添加到`window`对象上了

  
  
