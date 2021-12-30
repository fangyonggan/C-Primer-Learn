## 标准库类型string

### 1、初始化string

```c++
string s1; //默认初始化，s1是一个空串
string s2(s1);//s2是s1的副本
string s2 = s1;//等价于s2(s1),s2是s1的副本
string s3("value");//s3是字面量“value”的副本，除了字面量最后的那个空字符外
string s3 = "value"; //等价于s3("value")
string s4(n, 'f');//把s4初始化为由连续n个字符c组成的串
```

使用等号（=）初始化，执行的是拷贝初始化，不使用等号，则执行直接初始化

### 2、string对象上的操作

**读写string对象**

```c++
string s1, s2;
cin >>s1 >>s2; //把第一个输入读到s1中，第二个输入读到s2中
cout <<  s1 << s2 << endl;
```

**判断是否为空串empty**

empty返回True，代表字符串对象为空，否则，不为空

```c++
int main()
{
     string line;
     while (getline(cin, line))
     {
          if (line.empty())
          {
               return 0;
          }
          cout <<  line << endl;
     }

     return 0;
}
```

**字符串长度size**

size函数返回string对象的长度。

size函数返回的是一个string::size_type类型的值，string::size_type是一个无符号类型的值而且能够存放下string对象的大小。

```c++
string line = "fang";
cout <<  line.size() << endl;//输出为4
```

允许编译器通过auto推断变量的类型

```C
auto len = line.size();//len的类型是string::size_type
```

**string对象比较**

string类定义了几种用于比较字符串的运算符。这些比较运算符逐一比较string对象中的字符，大小写敏感。

相等性运算符（==和！=）分别检验两个string对象相等或者不相等，string对象相同意味着他们的长度相同且包含的字符也相同。

关系运算符<、<=、>、>=分别检验一个string对象是否小于，小于等于、大于、大于等于另一个string对象。

- 长度不同，较短string对象的每个字符与较长的对象对应为止的字符相同，叫说较短的string小于较长的string
- 如果两个string对象在某些对应的位置上不一致，则string对象的比较结果其实是string对象中第一对相异字符比较的结果。

**为string对象赋值**

直接用“=”符号赋值

**两个string对象相加**

相加得到一个新的string对象

```c++
     string s1 = "fang";
     string s2 = "yonggan";
     string s3 = s1 + s2; 
     cout <<  s3 << endl;//"fangyonggan"
```

**字面值和string对象相加**

当把string对象和字符串字面值及字符串字面值混在一条语句中使用时，必须确保每个加法运算器两侧的运算对象至少有一个是string。

```c++
string s2 = "fang";
string s1 = s2 +", ";
string s3 = "is" + " handsome";//错误，加号左右的对象都不是string
string s4 = s1 + "is handsome";//正确，必须至少有一个运算对象是string
string s5 = s1 + "is" + " handsome";//正确，等价于string tmp = s1 + "is";string s5 = tmp + " handsome";
string s5 = "is" + " handsome" + s1;//错误，字符串字面值不能直接相加
```

切记，字符串字面值与string不是同一类型！

### 处理string对象中的字符

关键在于获取字符本身。

**处理每个字符？使用基于范围的for语句**

范围for语句的语法格式：

```
for (declaration: expression)
{
	statement;
}
```

expression部分是一个对象，用于表示一个序列。

declaration部分负责定义一个变量，该变量将被用于访问序列中的基础元素。每次迭代，declaration部分的变量会被初始化为expression部分的下一个元素值。

```c++
string str("some string");
//每行输出str中的一个字符
for (auto a : str) //对于str中的每个字符
{
	cout << c << endl;//输出当前字符
}
```

**使用for语句改变字符串中的字符**

如果想要改变string对象中字符的值，必须把循环变量定义成引用类型。记住，所谓引用只是给定对象的一个别名，因此当使用引用作为循环控制变量时，这个变量实际上被一次绑定到了序列的元素上。使用引用，就能改变他绑定的字符！

```c++
#include <iostream>
#include <string>

using namespace std;

int main()
{
     string s1("fang yong gan");
     //转为大写字母
     for (auto &a : s1) //对于s1中的每个字符
     {
          if (isalpha(a)) //判断是否是字母
          { 
               a = toupper(a);//a是引用，因此赋值语句将改变s1中字符的值
          }
     }
     cout << s1 << endl;
     return 0;
}
```

**访问字符串中的单个字符**

两种方式

1. 使用下标
2. 使用迭代器

下标运算符[]接受的输入参数为string::size_type类型的值，这个参数表示要访问的字符的为止，返回值是该位置上字符的引用。

string对象的下标是从0开始，如果string对象s不为空，则s[0]是第一个字符，s[s.size()-1]是最后一个字符。

**string对象的下标必须大于等于0，而小于s.size()!**，超过此范围的下标将引发不可预知的结果，因此，使用下标访问空string也会引发不可预知的结果！所以在访问字符之前，首先要检查string对象是否为空！

```c++
string s("fang, good man");
if (!s.empty()) //确保s[0]的位置确实有字符
{
	s[0] = toupper(s[0]);//为s的第一个字符赋一个新值从
}
```

ps：注意检查下标的合法性

​	使用下标必须确保其在合理的范围内——大于等于0而小于字符串的size()的值。一种简便易行的方法是，总是设下标的类型为string::size_type，因为此类型是无符号数，可以确保下标>=0，此时，代码只要确保下标小于size()的值即可。

## 标准库类型vector

标准库类型vector表示**对象的集合**，引用不是对象，其中所有对象的类型都相同。集合中的每个对象都有一个与之对应的索引，索引用于访问对象。因为vector“容纳着”其他对象，所以它也常被称作容器（container）。

要想使用vector，必须包含适当的头文件。

```c++
#inclued <vector>
using std::vector;
```

vector是一个类模板。可以将模板看作编译器生成类或者函数编写的一份说明。编译器根据模板创建类或函数的过程称为实例化，当使用模板时，需要指出编译器应把类或者函数实例化成何种类型。

对于类模板来说，我们通过提供一些额外信息来指定模板到底实例化成什么样的类，需要提供哪些信息由模板决定。提供信息的方式总是这样：即在模板名字后面跟一对尖括号，在括号内放上信息。

**定义和初始化vector**

```c++
vector<T> v1; //v1是一个空vector，它潜在的元素是T类型的，执行默认初始化
vector<T> V2(V1) //V2中包含v1中所有元素的副本
vector<T> v2 = v1 //等价于v2(v1),v2包含v1所有元素的副本
vector<T> v3(n, val) //v3包含了n个重复的元素，每个元素的值都是val
vector<T> v4(n) //v4包含了n个重复地执行了值初始化的对象
vector<T> v5{a,b,c...} //v5包含了初始值个数的元素，每个元素被赋予相应的初始值
vector<T> v5 = {a,b,c...} //等价于v5{a,b,c...}
```

vector可以高效添加元素。最常见的定义方式就是先定义一个空vector，然后当运行时获取到元素的值后再逐一添加。

**列表初始化vector对象**

```c++
vector<string> articles = {"a", "an", "the"};
vector<string> v1{"a", "an", "the"};//列表初始化
```

**创建指定数量的元素**

vector对象容纳的元素数量和所有元素的统一初始值来初始化vector对象

```c++
vector<int> ivec(10, -1); //10个int类型的元素，每个都被初始化为-1
vector<string> svec(10, "hi"); //10个string类型的元素，每个都被初始化为"hi"
```

**值初始化**

通常情况下，可以只提供vector对象容纳的元素数量而略去初始值，此时库会创建一个**值初始化的**元素初值，并把它赋给容器中的所有元素。这个初值由vector对象中的元素的类型决定。

如果vector对象的元素是内置类型，比如int，则元素初始化自动设为0。如果是某种类类型，比如string，则元素由类默认初始化

```c++
vector<int> ivec(10); //10个int类型的元素，每个都被初始化为0
vector<string> svec(10); //10个string类型的元素，每个都是空对象
```

**向vector对象中添加元素**

**vector对象能高效增长：**

C++标准要求vector应该能在运行时高效快速地添加元素。因此既然vector对象能高效地增长，那么在定义vector对象的时候设定其大小也就没什么必要了，事实上如果定义时设定其大小性能可能更差。只有一种例外情况，就是所有元素的值都一样！一旦元素的值不同，更有效的办法是，再在运行时向其中添加具体值。

vector成员函数push_back：可以把一个值当成vector对象的尾元素“压到”（push）vector对象的“尾端”（back）

```c++
     vector<int> v2; //空vector对象
     for (int i = 0; i < 100; i++)
          v2.push_back(i); //依次把整数值放到v2尾端
     //循环结束后v2有100个元素，值从0到99
```

**其他vector操作**

```c++
v.empty()  //如果v不含有任何元素，返回真
v.size()  //返回v中元素的个数
v.push_back(t) //向v的尾部添加一个值为t的元素
v[n]  //返回v中第n个位置上元素的引用
v1 = v2   //用v2中元素的拷贝替换v1中的元素
v1 = {a,b,c...}  //用列表中元素的拷贝替换v1中的元素
v1 == v2  //v1和v1相等当且仅当他们的元素数量相同且对应位置的元素值都相同
```

vector的empty和size两个成员和string的同名成员功能完全一致，size返回类型是由vector定义的size_type类型。要想使用size_type，要首先指定它是由那种类型定义的！

```c++
vector<int>::size_type //正确
vector::size_type //错误
```

vector对象（以及string对象）的下标运算符可用于访问已经存在的元素，而不能用于添加元素

## 迭代器介绍

所有标准库容器都可以使用迭代器，但是只有少数几种才同时支持下标运算符[]。类似于指针类型，迭代器也提供了对对象的间接访问，就迭代器而言，其对象是容器中的元素或者string对象中的字符（严格来说，string不是容器类型），使用迭代器可以访问某个元素，迭代器也能从一个元素移动到另外一个元素。

迭代器有有效和无效之分，类似指针。**有效的迭代器或者指向某个元素，或者指向容器中尾元素的下一个位置，其他所有情况都是无效的！**

### 使用迭代器

和指针不同，获取迭代器不是使用取地址符，有迭代器的类型同事拥有返回迭代器的成员。比如，这些类型都拥有名为begin和end的成员，其中begin成员负责返回指向第一个元素（或第一个字符）的迭代器。end成员负责返回指向容器“尾元素的下一个位置”的迭代器，该迭代器指示的是容器的一个本不存在的“尾后”元素。这样的迭代器没什么实际意义，只是标记而已！

end成员返回的迭代器被称为尾（后）迭代器。如果容器为空，则begin和end返回的是同一个迭代器，都是尾后迭代器。

一般来说，我们不清楚（不在意）迭代器准确的类型到底是什么。

```c++
auto b = vec.begin(); //编译器决定b的类型
```

**迭代器运算符**

```c++
*iter                //对iter进行解引用，返回迭代器iter指向的元素的引用
iter->men            //对iter进行解引用，获取指定元素中名为men的成员。等效于(*iter).men
++iter                //给iter加1，使其指向容器的下一个元素
iter++
--iter                //给iter减1，使其指向容器的前一个元素
iter--
iter1==iter2        //比较两个迭代器是否相等，当它们指向同一个容器的同一个元素或者都指向同同一个容器的超出末端的下一个位置时，它们相等 
iter1!=iter2  
```

```c++
     string s("fang!");
     if (s.begin() != s.end()) //确保s非空
     {
          auto it = s.begin(); //it表示s的第一个字符
          *it = toupper(*it);   //改成大写字符
     }
```

**迭代器类型**

拥有迭代器的标准库类型使用iterator和const_iterator来表示迭代器的类型：

```c++
vector<int>::iterator it;   //it能读写vector<int>的元素
string::iterator it2;    //it2能读写string对象中的字符

vector<int>::const_iterator it3; //it3只能读元素，不能写元素
string::const_iterator it4;  //it4只能读字符，不能写字符
```

**begin和end运算符**

begin和end返回的具体类型由对象是否是常量决定，如果是常量，begin和end返回const_iterator,如果不是常量，返回iterator：

```c++
vector<int> v;
auto it1 = v.begin(); //it1的类型是vector<int>::iterator

const vector<int> cv;
auto it2 = cv.begin(); //it2的类型是vector<int>::const_iterator
```

如果对象只需读操作而无需写操作的话最好使用常量类型。为了便于专门得到const_iterator类型的返回值，C++ 11引入了两个新函数，分别为cbegin和csend：

```c++
vector<int> v;
auto it3 = v.cbegin(); //it3类型为vector<int>::const_iterator
```

不论vector对象（或者string对象）本身是否是常量，返回值都是const_iterator.

