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
