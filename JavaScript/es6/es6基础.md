# 变量的声明
  
>es5声明变量  

+ var声明：不能声明块级作用域变量

>es6声明变量

+ let声明：可以声明块级作用域的变量
+ const:
>语法优势

1. 不存在变量提升  

    >变量提升:变量在声明之前使用，值为underfunded   
    
    >let语法改变了语法行为，使用变量一定要在声明变量之后，否则会报错  
2. 暂时性死区

    >使用let声明变量之前，该变量都是不可用的，在语法上成为暂时性死区  
    
    >区块中存在let和const命令，区块对这些命令声明的变量从一开始就形成了封闭的作用域，凡是在之前使用这些变量，就会报错  
    
    >变量在声明之前都属于“死区”，只要用到就报错，因此在typeof运行时可能会报ReferenceError

3. 不允许重复声明
    
    >不允许在相同的作用域内，重复声明同一个变量，会报错  
    
    >不能再函数内重新声明参数  
    
>块级作用域  

1. es5的作用域

    > es5只有全局作用域和函数作用域，没有块级作用域    
    
      不合理的场景：  
        
        

































