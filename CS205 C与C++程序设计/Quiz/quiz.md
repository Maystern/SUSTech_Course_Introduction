# CS205 C/CPP Design Quiz

1. The source code of program is as follows:

   ```cpp
   int main(int arc, char *argv[]) {
       ...
   }
   ```

   The source code has been compiled to program ***hello***, when you run it as follows, what ***argc*** will be ?

   ```
   ./hello I LOVE CPP
   ```

   【分析】在使用 `int main(int arc, char *argv[])` 时，数组 ***argv*** 从下标 $0$ 开始依次存储输入的编译参数，而 ***arc*** 则记录输入编译参数的个数，本题中输入参数为`./hello I LOVE CPP` 有 $4$ 个编译参数，`./hello`、`I`、`LOVE`、`CPP` ，因此  ***arc*** 的值为 $4$。

   【答案】4

2. The following code is the ***prototype/declaration*** of function ***mul***.

   ```cpp
   int mul(int a, int b) {
       return a * b;
   }
   ```

   【分析】***prototype/declaration*** 表示声明，***definition*** 表示定义。上述代码是函数 ***mul*** 的定义而非声明，所以陈述错误。声明应该改写为：

   ```cpp
   int mul(int a, int b);
   ```

    【答案】False

3. The data type of the variable ***PI*** is ***double***.

   ```cpp
   #define PI 3.14
   ```

   【分析】***PI*** 并不是变量（***variable***），虽然宏定义默认的小数是使用***double*** 类型存储的，所以陈述错误。

   【答案】False

4. When a function prototype is declared in the header file you create, you do NOT need to define it in a CPP file.

   【分析】进行声明（***prototype***）后，还需要进行定义（***definition***）。使用未定义但已经声明的函数时，程序可以通过编译（***compile***），但是会导致连接错误（***Link Error***），无法生成可执行文件。因此，为了实现程序功能，函数既要有声明又需要有定义，所以陈述错误。

   【答案】False

5. IDE (Integrated development environment) is a powerful compiler with many useful features.

   【分析】IDE，即集成开发环境，是用于提供程序开发环境的应用程序。集成了代码的编写、分析、编译、调试多种功能。而编译器，是将代码（通常为高级语言）翻译成为另外一种语言（通常为低级语言），便于计算机进行执行的程序。IDE中集成了编译器，因此 IDE 不是编译器，陈述错误。

   【答案】False

6. If you get 75 for one of your projects, which situation should most likely be?

   A. Finish all tasks almost perfectly

   B. Finish all tasks well

   C. Correct

   D. Finish all tasks

   【分析】根据于仕琪老师第一节课程的ppt，project评分有如下等级：

   - 90 - 100 : Finish all tasks almost perfectly.
   - 80 - 90 :  Finish all tasks well.
   - 70 - 80 :  Finish all tasks.

   因此，75 分对应的是 70 - 80 分档，应该属于`Finish all tasks` 情形，选D。

   【答案】D

7. What's the output of the source code?

   ```cpp
   signed char c1 = 127;
   signed char c2 = 1;
   int csum = c1 + c2;
   cout << csum;
   ```

   【分析】在运行程度段时，由于 `signed char` 是 8 位有符号整数，最大可以表示数字的范围是$[-128, 127]$。执行 `int csum = c1 + c2` 语句时，自动转换为 `int` 类型进行计算，因此会返回正确结果 $128$，而不会产生溢出。

   【答案】128

8. `sizeof()` is a function and can yield the size in bytes of a type. 

   ```cpp
   int int_num = 10;
   size_t len = sizeof(int_num);
   ```

   【分析】`sizeof` 是一个操作符，并不是一个函数，故陈述错误。

   【答案】False

9. `size_t` is an unsigned integer type.

   【分析】`size_t` 是 32 位或 64 位无符号整数，陈述正确。

   【答案】True

10. What's the value of the variable ***num1, num2, num3***?

   ```cpp
int num1 = 23 / 4 * 4;
int num2 = 23 / 4 * 4.;
int num3 = 23 / 4. * 4;
   ```

   【分析】首先计算 ***num1***，从左到右依次计算，先计算`23 / 4`，由于两个操作数 $23, 4$ 都是 `int` 类型，所以执行整数除法运算，答案为 `5`，同理再计算 `5 * 4` 得到答案 20；

   ​				然后计算 ***num2***，从左到右依次计算，先计算`23 / 4`，由于两个操作数 $23, 4$ 都是 `int` 类型，所以执行整数除法运算，答案为 `5`，再计算 `5 * 4.`，操作数`4.`是`float`类型，执行浮点数乘法运算，得到答案 `20.`由于隐式类型转换 float 转换为 int类型不产生整数部分的误差，所以得到答案 $20$；

   ​				最后计算 ***num3***，从左到右依次计算，先计算`23 / 4.`，由于操作数 $4$ 都是 `float` 类型，所以执行浮点数除法运算，答案为 `5.75f`，再计算 `5.75f * 4`，操作数`5.75f`是`float`类型，执行浮点数乘法运算，得到答案 `23.`由于隐式类型转换 float 转换为 int类型不产生整数部分的误差，所以得到答案 $23$。

   【答案】***num1 = 20；num2 = 20；num3 = 23***

11.  In the following code, since the variable num is not initialized explicitly, it will be initialized to 0 automatically.

     ```cpp
     int num;
     cout << num << endl;
     ```

     【分析】在 $C++$ 中，未初始化的变量将会根据编译器的不同赋随机值，并非一定为 0，所以陈述错误。

     【答案】False

12.  auto is a placeholder type specifier in C++11. What is the value of the variable ***val*** in the following code?

     ```cpp
     auto val = 2 / 3;
     val = 3.14 * 2;
     ```

     【分析】在执行语句`auto val = 2 / 3;`时，由于操作数 $2, 3$ 都是 `int` 类型，所以执行整数除法运算，得到结果`(int) 0`，所以变量 ***val*** 的类型为 `int`。在执行语句`val = 3.14 * 2;`时，先计算 `3.14 * 2` 执行浮点数乘法运算，得到结果`6.28f`，赋值时进行隐式类型转换，float 转换为 int 不产生整数部分的误差，因此执行所有语句后变量 ***val*** 的值为 $6$。

     【答案】6

13.  What's the output of the following source code ?

     ```cpp
     int x = 100;
     int y = 30;
     x += (y -= 10);
     cout << x;
     ```

     【分析】执行 `x += (y -= 10);` 时先执行`y -= 10`，执行完毕后 $y$ 的值为 20，作为 `(y -= 10)`的返回值，再执行 `x += 20`，执行完毕后 $x$ 的值为 $120$。

     【答案】120

14.  What's the output of the following source code ?

     ```cpp
     int x = 100;
     int y = x++;
     cout << y;
     ```

     【分析】先执行 `y = x` 的赋值，再执行自增`x++`。执行完毕后，$x$ 的值为 101，$y$ 的值为100。

     【答案】100

15.  What's the output of the following source code ?

     ```cpp
     int x = 100;
     int y = (x = 200);
     cout << y;
     ```

     【分析】先执行 `x = 200` 的赋值，将 $200$ 作为`(x = 200)`的返回值，再执行赋值`y = 200`。执行完毕后，$x$ 的值为 200，$y$ 的值为 200。

     【答案】200

16.  What's the output of the following source code ?

     ```cpp
     int a = 2, b = 0;
     if (a || b++) {
         cout << b;
     }
     ```

     【分析】`a` 的值为 2，隐式转化为 `bool` 值为 true，由于短路效应，`b++` 未被执行，因此输出 $b$ 的值为 0；若将上述代码改为：

     ```cpp
     int a = 2, b = 0;
     if (b++ || a) {
         cout << b;
     }
     ```

     则由于判断时先执行`b++`（false） 再逻辑或`a`（true），判断完毕后 $b$ 自增，因此输出 $b$ 的值为 1。

     【答案】0

17.  What's the output of the following source code ?

     ```cpp
     int i = 0;
     for (i = 1; i < 100; i += 2) {
         // something
     }
     cout << i
     ```

     【分析】循环变量 $i$ 的初始值为 1，每次循环累加 2，最后一次执行循环中内容时，$i = 99$。循环结束时，$i$ 自增 2，输出 101。

     【答案】101

18.  What's the output of the source code ?

     ```cpp
     int x = 5;
     do {
         x = 0;
     } while (x);
     cout << x;
     ```

     【分析】赋值完毕后直接进入 do-while 循环，赋值`x = 0`，判断条件 $x$ 为false，因此输出 0。

     【答案】0

19.  The following source code (empty in the parentheses) can be compiled successfully.

     ```cpp
     for () {
         // some lines here
     }
     ```

     【分析】for 循环语句必须使用两个`;`分隔开初始语句、条件语句、累加语句，不能缺漏，因此陈述错误。

     【答案】False

20.  What is the output of the following code ?

     A. Key 4

     B. Key 5

     C. Undefined key.

     ```cpp
     int num = 5;
     switch (num) {
         case '4':
             cout << "Key 4" << endl;
         case '5':
             cout << "Key 5" << endl;
         default:
             cout << "Undefined key."
     }
     ```

     【分析】`'4'` 对应是相关字符，并不是数字，`int`与`char` 比较都应该转化为`int`，所以应该输出 "Undefined key."，选择 C。

     【答案】C

21.  How many lines will be printed ?

     A. Compilation error

     B. 10

     C. 11 
     D. None of the above

     ```cpp
     for (size_t i = 10; i >= 0; i--)
         cout << "Line " << i << endl;
     ```

     【分析】`size_t` 是 32 位或 64 位无符号整数，会自然溢出，所以条件`i >= 0` 永远成立，因此将输出无限行，并非编译错误，10 或者 11行，所以选择 D。

     【答案】D

22.  What's the output of the source code?

     A. 2

     B. 4

     C. 6

     D. 8

     E. The source code cannot be compiled without error.

     F. Unpredictable result.

     ```cpp
     #include <iostream>
     using namespace std;
     int main() {
         int idx = 0;
         int numbers[4] = {2, 4, 6, 8};
         idx = -1;
         cout << numbers[idx];
     }
     ```

     【分析】由于 C++ 在数组访问下标时，不会对下标进行检查，所以将使得访问未知内容，输出不可预测值。

     【答案】F

23.  What's the output of the source code?

     A. 2

     B. 4

     C. 6

     D. 8

     E. The source code cannot be compiled without error.

     F. Unpredictable result.

     ```cpp
     #include <iostream>
     using namespace std;
     int main() {
         int idx = 0;
         int numbers[4] = {2, 4, 6, 8};
         idx = 4;
         cout << numbers[idx];
     }
     ```

     【分析】由于 C++ 在数组访问下标时，不会对下标进行检查，数组下标从 $0$ 开始，因此将使得访问未知内容，输出不可预测值。

     【答案】F

24.  What's the output if you compile the following source code with C++11 standard?

     ```cpp
     char str[16] = {"C++"};
     cout << strlen(str) << endl;
     ```

     【分析】使用 C++ 11 标准 `char str[16] = {"C++"};` 是合法的字符数组定义，`str[0] = 'C'`，`str[1] = str[2] = '+', str[3] = '\0'`，执行 `strlen(str)` 计算从字符串开始到 `'\0'` 前一个字符的个数，即 3 个。

     【答案】3

25.   What's the output if you compile the following source code with C++11 standard?

     ```cpp
     char str {"C++"};
     cout << str[1] << endl;
     ```

     【分析】使用 C++ 11 标准 `char str {"C++"};` 是合法的字符数组定义，`str[0] = 'C'`，`str[1] = str[2] = '+', str[3] = '\0'`，下标从$0$开始，`str[1]` 访问从字符串的第 1 号字符，即 `'e'`。

     【答案】 e

26.  What's the output?

     A. C++

     B. No output.

     C. Compilation error.


     D. Runtime error.

     ```cpp
     char str1[16] = {"C++"};
     char str2[16];
     str2 = str1;
     cout << str2;
     ```

     【分析】使用 C++ 11 标准 `char str1[16] = {"C++"};` 是合法的字符数组定义，`str1[0] = 'C'`，`str1[1] = str1[2] = '+', str1[3] = '\0'`，`char str2[16];` 也是合法的字符数组定义，`str2[0] = '\0'`。字符数组不能使用`str2 = str1` 赋值，因此将会出现编译错误。

     【答案】C

27.  What's the output?

     A. C++

     B. No output.

     C. Compilation error.

     D. Runtime error.

     ```cpp
     string str1 = {"C++"};
     string str2;
     str2 = str1;
     cout << str2;
     ```

     【分析】使用 C++ 11 标准 `string str1 = {"C++"};` 是合法的字符串定义，`str1 = "C++"`，`char str2[16];` 也是合法的字符数组定义，`str2 = ""`。字符串能使用`str2 = str1` 赋值，因此输出 C++。

     【答案】A

28.   What's the output?

     ```cpp
     #include <iostream>
     union twonumbers {
         int n[2];
         double d;
     };
     using namespace std;
     int main () {
         twonumbers tn;
         tn.n[0] = 0;
         tn.n[1] = 0;
         cout << tn.d;
         return 0;
     }
     ```

     【分析】根据 union 的特性，`int n[2]` 和 `double d` 共用一个大小为 8 字节的内存空间。`tn.n[0] = 0;` 将前 4 字节的内容清空为0， `tn.n[1] = 0;` 将后 4 字节的内容清空为0。所以整个内存空间被清空为$0$。所以该内存空间表示的浮点数为 $0$。

     【答案】0

29.  The output of the following code is:

     ```cpp
     struct Person {
         bool male;
         int id;
         char label;
     }
     cout << sizeof(struct Person);
     ```

     【分析】`struct` 在 C++ 中以 4 个字节对齐（1个字节的向后补齐，4 个字节以上必须是按照 4 字节对齐），male 占 1 个字节，id 占 4 个字节，label 占 1 个字节。所以实际消耗内存 4 + 4 + 4 = 12 字节，输出 12。

     【答案】12

30.   What's the output of the following code?

     ```cpp
     int *numbers = new int[8];
     char *pc = (char *) numbers;
     *numbers = 0x0A0B0C0D;
     cout << (int) pc[3];
     ```

     【分析】`int *numbers = new int[8];` 语句开辟了 $8 \times 4$ 字节的空间用于存储 $8$ 个 int 类型的值。`char *pc = (char *) numbers;` 将 `pc` 指针指向`numbers` 的首地址（由于是 `char*`类型，所以`pc[3]` 指的是从左往右第 $4$ 个字节的 `char` 类型的数字）。`*numbers = 0x0A0B0C0D;` 将 `numbers` 的值设为 16 进制的 `0A0B0C0D`，即二进制的`0000 1010 0000 1011 0000 1100 0000 1101`，每 1 个字节（即 8 个比特）为一组，从低位到高位依次是：`00001101`、`00001100`、`00001011`、`00001010`、`00000000`... 。因此，`pc[3]` 表示的是 `00001010`，使用 `(int)` 进行隐式类型转换为 `10`。

     【答案】10

31.   The following source code is correct.

     ```cpp
     int *ptr;
     *ptr = 3;
     ```

     【分析】由于 `int *ptr;` 定义一个空指针，并未赋值地址，因此也不能将对应地址指向的元素值置为 $3$，执行该段代码后会导致段错误。

     【答案】False

32.   What's the output of the following code on your PC (64 bit OS and CPU)?

     ```cpp
     int numbers[8];
     cout << sizeof(numbers) << endl;
     ```

     【分析】`int` 类型占 4 字节，开辟 8 个形成 `numbers` 数组，共占用 32 个字节。

     【答案】32

33.   What's the output of the following code on your PC (64 bit OS and CPU)?

     ```cpp
     int *numbers = new int[8];
     cout << sizeof(numbers) << endl;
     ```

     【分析】`int *numbers = new int[8];` 将开辟 8 个`int` 类型的数组变量的首地址传给`numbers`，作为地址变量，其类型为 `size_t`，当前系统是 64 bit（即 8 字节），所以`size_t` 所占空间为 8 字节。

     【答案】8

34.  The following code can be compiled successfuly.

     ```cpp
     double value = 0.0;
     const double *p = &value;
     value = 2.0;
     ```

     【分析】`const double *p = &value;`指的是无法使用 $p$ 指针更改 `val` 的值，若不通过 $p$ 指针直接修改 `value` 的值，可以修改成功。

     【答案】True

35.   The following code can be compiled successfuly.

     ```cpp
     double value = 0.0;
     double * const p = &value;
     p[0] = 2.0;
     ```

     【分析】`double * const p = &value;`指的是无法更改 $p$ 指针指向的地址，`p[0] = 2.0` 等价于 `*p = 2.0`，若通过 $p$ 指针修改 `value` 的值，可以修改成功。

     【答案】True

36.  The following source code is correct and cannot cause bugs.

     ```cpp
     int *pint = (int *) malloc(8 * sizeof(int));
     char * pc = (char *) pint;
     pc[8] = 'a';
     *(pc + 8) = 'b';
     ```

     【分析】`int *pint = (int *) malloc(8 * sizeof(int));` 开辟了 8 个 `int` 类型变量的空间。`char * pc = (char *) pint;` 使用 `char` 指针，指向 `pint` 所指向的空间处。对 `pc[8]` 和 `*(pc + 8)` 赋值都对应 `pc` 从首地址开始向后第 8 个字节，进行赋值。显然开辟了 8 个 `int` 类型变量的空间就意味着开辟了 $8 \times 4$ 个字节的空间，因此程序可以运行。

     【答案】True

37.  
