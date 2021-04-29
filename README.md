# do_while_0_explanation

```
为什么宏定义里面的函数调用都用do while 0包起来.

如果1.我们用括号来写宏定义
  例子:
  #define SAFE_FREE(p)  { free(p); p=NULL; }
  int *p =NULL;
  if(NULL!=p)

     SAFE_FREE(p);

  else{
  };
  会报错.因为if 里面的语句替换后带了;所以他就结束了if 整个语句.下面else会找不到对应的if

  例子:
  #define SAFE_FREE(p)  { free(p); p=NULL; }
  int *p =NULL;
  if(NULL!=p)

     SAFE_FREE(p)

  else{
  };
  如果我们这么写if里面调用的SAFE_FREE后面没有;也是错的,因为不符合c语言规范.当然跑起来是对的.这里面说错是因为当一个人不知道他是宏函数而认为他是一个普通函数时候后面就加分号了.
  综上我们得到结论在宏定义函数里面写括号包起来是错误的.如果不用括号显然更错误.
  所以我们用do while 0语句
  正确写法:
  
  #define SAFE_FREE(p)  do{ free(p); p=NULL; }while(0)
  int *p =NULL;
  if(NULL!=p)

     SAFE_FREE(p);

  else{
  };
  
  成功编译成功了.
  
  
  宏替换之后的效果看看:

  int *p =NULL;
  if(NULL!=p)

     do{ free(p); p=NULL; }while(0);

  else{
  };
  也是编译成功的!!!!!!!!!!!!!!!!!!!!!!!!
```











