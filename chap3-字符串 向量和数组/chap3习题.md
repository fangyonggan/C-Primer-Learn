## 练习3.2

编写一段程序从标准输入中一次读入一行，然后修改该程序使其一次读入一个词。

解：

一次读入一行：

```c++
#include <iostream>
#include <string>

using std::string;
using std::cin;
using std::cout;
using std::endl;
using std::getline;

int main()
{
	string s;
	while (getline(cin,s))
	{
		cout << s << endl;
	}
	return 0;
}
```


一次读入一个词

```c++
#include <iostream>
#include <string>

using std::string;
using std::cin;
using std::cout;
using std::endl;
using std::getline;

int main()
{
	string s;
	while (cin >> s)
	{
		cout << s << endl;
	}
	return 0;
}
```

## 练习3.3

请说明string类的输入运算符和getline函数分别是如何处理空白字符的。

解：

- 类似is >> s的读取：string对象会忽略开头的空白并从第一个真正的字符开始，直到遇见下一空白为止。
- 类似getline(is, s)的读取：string对象会从输入流中读取字符，直到遇见换行符为止。

练习3.4
编写一段程序读取两个字符串，比较其是否相等并输出结果。如果不相等，输出比较大的那个字符串。改写上述程序，比较输入的两个字符串是否等长，如果不等长，输出长度较大的那个字符串。

```c++
#include <iostream>
#include <string>
using std::string;
using std::cin;
using std::cout;
using std::endl;

int main()
{
	string str1, str2;
	while (cin >> str1 >> str2)
	{
		if (str1 == str2)
			cout << "The two strings are equal." << endl;
		else
			cout << "The larger string is " << ((str1 > str2) ? str1 : str2);
	}

	return 0;
}
```

 长度大的 

```c++
#include <iostream>
#include <string>
using std::string;
using std::cin;
using std::cout;
using std::endl;

int main()
{
	string str1, str2;
	while (cin >> str1 >> str2)
	{
		if (str1.size() == str2.size())
			cout << "The two strings have the same length." << endl;
		else
			cout << "The longer string is " << ((str1.size() > str2.size()) ? str1 : str2) << endl;
	}

	return 0;
}
```

## 练习3.5

编写一段程序从标准输入中读入多个字符串并将他们连接起来，输出连接成的大字符串。然后修改上述程序，用空格把输入的多个字符串分割开来。

解：

未隔开的：

```c++
#include <iostream>
#include <string>

using namespace std;

int main()
{
     string s1;
     string res;
     while (cin >> s1)
     {
          if (s1 == "q!"){
               break ;
          }
          res = res + s1;
     }
     cout << res << endl;
     return 0;
}
```

隔开的

```c++
#include <iostream>
#include <string>

using namespace std;

int main()
{
     string s1;
     string res;
     while (cin >> s1)
     {
          if (s1 == "q!"){
               break ;
          }
          res = res + s1 + " ";
     }
     cout << res << endl;
     return 0;
}
```

## 练习3.6

编写一段程序，使用范围for语句将字符串内所有字符用X代替。

```c++
#include <iostream>
#include <string>

using namespace std;

int main()
{
     string s1 = "hello world!";
     /* 使用下标和for循环
     string::size_type index = 0;
     for (; index < s1.size(); index++)
     {
     s1[index] = 'X';
     }
     */
     for (auto &a : s1) //for语句
     {
          a = 'X';
     }
     cout << s1 << endl;
     return 0;
}
```

## 练习3.7

就上一题完成的程序而言，如果将循环控制的变量设置为char将发生什么？先估计一下结果，然后实际编程进行验证。

解：

如果设置为char而不是引用，那么原来的字符串不会发生改变。

## 练习3.9

下面的程序有何作用？它合法吗？如果不合法？为什么？

```c++
string s;
cout << s[0] << endl;
```

解：

不合法。使用下标访问空字符串是非法的行为。

## 练习3.10

编写一段程序，读入一个包含标点符号的字符串，将标点符号去除后输出字符串剩余的部分。

```c++
#include <iostream>
#include <string>

using namespace std;

int main()
{
     string s1 = "this, is. a :string!";
     string s2;
     for (auto a : s1){
          if (!ispunct(a))
               s2 += a;
     }
     cout << s2 << endl;
     return 0;
}
```

## 练习3.11

下面的范围for语句合法吗？如果合法，c的类型是什么？

```c++
const string s = "Keep out!";
for(auto &c : s){ /* ... */ }
```

解：

要根据for循环中的代码来看是否合法，c是string 对象中字符的引用，s是常量。因此如果for循环中的代码重新给c赋值就会非法，如果不改变c的值，那么合法。

## 练习3.12

下列vector对象的定义有不正确的吗？如果有，请指出来。对于正确的，描述其执行结果；对于不正确的，说明其错误的原因。

```c++
vector<vector<int>> ivec;         // 在C++11当中合法
vector<string> svec = ivec;       // 不合法，类型不一样
vector<string> svec(10, "null");  // 合法
```

## 练习3.13

下列的vector对象各包含多少个元素？这些元素的值分别是多少？

```c++
vector<int> v1;         // size:0,  no values.
vector<int> v2(10);     // size:10, value:0
vector<int> v3(10, 42); // size:10, value:42
vector<int> v4{ 10 };     // size:1,  value:10
vector<int> v5{ 10, 42 }; // size:2,  value:10, 42
vector<string> v6{ 10 };  // size:10, value:""
vector<string> v7{ 10, "hi" };  // size:10, value:"hi"
```

## 练习3.17

从cin读入一组词并把它们存入一个vector对象，然后设法把所有词都改为大写形式。输出改变后的结果，每个词占一行。

解：

```c++
#include <iostream>
#include <vector>
#include <string>

using namespace std;

int main()
{
     vector<string> v2; //空vector对象
     string tmp;
     while(cin >> tmp)
     {
          if (tmp == "q!"){
               break;
          }
          v2.push_back(tmp);
     }
     for (auto &a : v2)
     {
          for (auto &b : a)
          {
               b = toupper(b);
          }
          //cout << a << endl;
     }
     for (auto s : v2){
          cout << s << endl;
     }
     return 0;
}
```

## 练习3.18

下面的程序合法吗？如果不合法，你准备如何修改？

```c++
vector<int> ivec;
ivec[0] = 42;
```

解答：

不合法。ivec是空的，不能通过索引添加元素，ivec[0]不合法，应改为

```c++
vector<int> ivec;
ivec.push_back(42);
```

## 练习3.19

如果想定义一个含有10个元素的vector对象，所有元素的值都是42，请例举三种不同的实现方法，哪种方式更好呢？

解：

```c++
vector<int> ivec1(10,42); //相同元素值，推荐这种
vector<int> ivec2{ 42, 42, 42, 42, 42, 42, 42, 42, 42, 42 };
vector<int> ivec3;
for (int i = 0; i < 10; ++i)
	ivec3.push_back(42);
```

## 练习3.20

读入一组整数并把他们存入一个vector对象，将每对相邻整数的和输出出来。改写你的程序，这次要求先输出第一个和最后一个元素的和，接着输出第二个和倒数第二个元素的和，以此类推。

解：

```c++
#include <iostream>
#include <string>
#include <cctype>
#include <vector>

using std::cin;
using std::cout;
using std::endl;
using std::vector;
using std::string;

int main()
{
	vector<int> ivec;
	int i;
	while (cin >> i)
	{
		ivec.push_back(i);
	}

	for (int i = 0; i < ivec.size() - 1; ++i)
	{
		cout << ivec[i] + ivec[i + 1] << endl;
	}
	
	//---------------------------------
	cout << "---------------------------------" << endl;
	
	int m = 0;
	int n = ivec.size() - 1;
	while (m < n)
	{
		cout << ivec[m] + ivec[n] << endl;
		++m;
		--n;
	}
	return 0;
}
```

## 

