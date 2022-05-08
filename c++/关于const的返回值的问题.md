# 1. 返回一个引用类型

Q：如果返回一个引用， 那是不是这个新的对象就是等于调用重载运算符的地址

A：傻x， 返回来只是为了效率，返回引用，你return的时候就不用调用一个拷贝构造来给这个临时对象，然后结束这个函数的时候，对其新对象调用拷贝构造就行了



另外再强调一下，值是怎么返回的，类似初始化一个变量，返回的值用于初始化调用点的一个临时量(临时对象)，

```cpp
#include <iostream>
#include <algorithm>
using namespace std;

class A {
public:
	int num;
	A(int x = 0):num(x) {
		cout << "A()\n";
	}
	A(A& obj) {
		cout << "A(A & obj)\n";
	}
	~A() {
		cout << "~A()\n";
	}
	A& operator + (A& rhs) 
	{
		num += rhs.num;
		return *this;
	}
	A& operator = (A& rhs) {
		num = rhs.num;
		cout << "A& operator = (A& rhs)\n";
		return *this;
	}
};


int main()
{
	A a(3); //A() 009BFDA8
	cout << &a << "\n";
	A b(4); //A() 009BFD9C
	cout << &b << "\n";
	A c;	//A() 009BFD90
	cout << &c << "\n";
    
	A d = c = a + b;  
	/* 
	1.+, 
	2.A& operator = (A& rhs)  
	3.A(A & obj) 返回的值用来拷贝构造
	这就是为啥 oprator= 要返回 A&类型， 如果是A也行， 那要重新拷贝构造一个对象， 所以效率上说，		返回引用节省了这个操作
	
	如果将表达式变成 A& d = a + b;
	那么 d 和 a 就是同一个对象，d 是 a 的别名
	*/
	cout << &d << "\n";//009BFD84
    
    cout << "--------------\n";
	cout << &(a + b) << "\n";
	cout << &(a + b) << "\n";	
	cout << &(a + b) << "\n"; //A() 009BFDA8
	//  这里就更加说明， 返回的是调用重载运算符的对象的地址，也就是a的地址
	cout << "--------------\n";
    
	return 0;
}	
```

