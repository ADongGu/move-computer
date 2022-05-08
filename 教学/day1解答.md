1.

## 题目描述

用高精度计算出 S = 1!+2!+3!+⋯+*n*!（*n*≤50）。

其中“!”表示阶乘，例如：5!=5×4×3×2×1。

#### 输出格式

一个正整数 S，表示计算结果。

样例输入输出：

```
输入：
3
输出：
9
```



2.

## 题目描述

现在有 *n*(*n*≤1000) 位评委给选手打分，分值从 0 到 10。需要去掉一个最高分，去掉一个最低分（如果有多个最高或者最低分，也只需要去掉一个），剩下的评分的平均数就是这位选手的得分。现在输入评委人数和他们的打分，请输出选手的最后得分。

样例输入输出：

```
输入：
5
9 5 6 8 9

输出：
7.67

#include <iostream>
#include <algorithm>
using namespace std;

int main() {

	int ma = -1, mi = 1000000009, sum = 0;
	int n; cin >> n;
	int val;
	for (int i = 1; i <= n; i++) {
		 cin >> val;
		 ma = max(val, ma);
		 mi = min(val, mi);
		 sum += val;
	}
	sum -= ma + mi;
	cout << (sum * 1.0) / (n - 2); 
	//  为什么要*1.0， 因为整形除法会向下取整，比如5/2 = //2,6/4 = 1...，
	// 然后这里*了1.0，就是转成浮点型， 这样就可以解决这个情况
	return 0;
}
```

这个直接说说思想吧， 你要取最低分，最高分，是不是要记录这两个变量，然后总数减去这两个值，求平均值就行





3.

## 题目描述

给定一个整数，请将该数各个位上数字反转得到一个新数。新数也应满足整数的常见形式，即除非给定的原数为零，否则反转后得到的新数的最高位数字不应为零。

样例输入输出：

```
输入：
123
输出
321

#include <iostream>
#include <algorithm>
using namespace std;

int main() {
	int n; cin >> n;
	while (n) {
		cout << n % 10;
		n /= 10;
	}
	return 0;
}
```

![image-20220419121345292](C:\Users\hzd\AppData\Roaming\Typora\typora-user-images\image-20220419121345292.png)