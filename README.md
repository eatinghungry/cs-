# cs-PAT

##为考研准备的刷题文件：
每天一道题吧

###2019.11.7
####   1001 A+B Format (20 分)


Calculate a+b and output the sum in standard format -- that is, the digits must be separated into groups of three by commas (unless there are less than four digits).


Input Specification:

Each input file contains one test case. Each case contains a pair of integers a and b where −10​6​​≤a,b≤10​6​​. The numbers are separated by a space.
Output Specification:

For each test case, you should output the sum of a and b in one line. The sum must be written in the standard format.
Sample Input:

-1000000 9

Sample Output:

-999,991
```c++
#include<iostream>
#include<iomanip>
using namespace std;
int main()
{
  long int m=0,n=0;
  int sum;
  if((m>=-1000000)&&(m<=1000000)&&(n>=-1000000)&&(n<=1000000))
  {
    cin>>m>>n;
    sum=m+n;
	if(sum<0)
	{
		cout<<"-";
		sum=-sum;
	}
	if(sum/1000000)
		cout<<sum/1000000<<","<<right<<setw(3)<<setfill('0')<<sum/1000%1000<<","<<right<<setw(3)<<setfill('0')<<sum%1000<<endl;
    else if(sum/1000)
    	cout<<sum/1000<<","<<right<<setw(3)<<setfill('0')<<sum%1000<<endl;
    else
      cout<<sum<<endl;
  }
  else
	  return 0;
  return 0;
}
```
***
***
### 2020.1.11（java）
[网址] https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/solution/wu-zhong-fu-zi-fu-de-zui-chang-zi-chuan-by-leetcod/ "leetcode"
####  给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。
##### 暴力法
###### 思路 :逐个检查所有的子字符串，看它是否不含有重复的字符。
假设我们有一个函数 boolean allUnique(String substring) ，如果子字符串中的字符都是唯一的，它会返回 true，否则会返回 false。
我们可以遍历给定字符串 s 的所有可能的子字符串并调用函数 allUnique。 如果事实证明返回值为 true，那么我们将会更新无重复字符子串的最大长度的答案。
java的hashset集合
```
HashSet<String> hashSet = new HashSet<String>();
/*HashSet实现Set 接口，由哈希表（实际上是一个 HashMap 实例）支持。它不保证集合的迭代顺序；特别是它不保证该顺序恒久不变。此类允许使用 null 元素。HashSet为基本操作提供了稳定性能，这些基本操作包括 add、remove、contains 和 size，假定哈希函数将这些元素正确地分布在桶中。
leetcode题解中给出了一个窗口滑动的概念，应该是字符串中比较常用的一个操作*/
charAt 返回索引处的字符
```

```
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        int n = s.length();
        int ans = 0;
        for (int i = 0; i < n; i++)
            for (int j = i + 1; j <= n; j++)
                if (allUnique(s, i, j)) ans = Math.max(ans, j - i);
        return ans;
    }

    public boolean allUnique(String s, int start, int end) {
        Set<Character> set = new HashSet<>();
        for (int i = start; i < end; i++) {
            Character ch = s.charAt(i);
            if (set.contains(ch)) return false;
            set.add(ch);
        }
        return true;
    }
}
```
##### 窗口滑动
###### 

```
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        int n = s.length();  //判断字符串的长度
        Set<Character> set = new HashSet<>();  //创建hashset集合，可以判断是否有重复字符
        int ans = 0, i = 0, j = 0;   //设置初值，ans用来返回最大长度，i是窗口左边界，j是窗口右边界
        while (i < n && j < n) {
            // try to extend the range [i, j]   //窗口右边界的右滑动
            if (!set.contains(s.charAt(j))){    //如果没有重复字符
                set.add(s.charAt(j++));         //窗口右边界的右滑动 就把当前字符加入集合中
                ans = Math.max(ans, j - i);	 //把已知的长度和当前长度对比
            }
            else {
                set.remove(s.charAt(i++));      //如果下一个字符是重复的，左边界右移动一个位置，并且从集合中移除该元素
		 //i++ 是先执行后加 ++i 是先加后执行 卡了好久
            }
        }
        return ans;
    }
}
```
##### 窗口滑动的优化
[hashmap和hashset的区别]https://blog.csdn.net/chen213wb/article/details/84647179
```
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        int n = s.length(), ans = 0;
        Map<Character, Integer> map = new HashMap<>(); // current index of character 有顺序的哈希
        // try to extend the range [i, j]
        for (int j = 0, i = 0; j < n; j++) {
            if (map.containsKey(s.charAt(j))) {
                i = Math.max(map.get(s.charAt(j)), i);
            }
            ans = Math.max(ans, j - i + 1);
            map.put(s.charAt(j), j + 1);
        }
        return ans;
    }
}
```
