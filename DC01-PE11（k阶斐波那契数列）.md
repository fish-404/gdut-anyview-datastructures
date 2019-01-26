>【题目】已知k阶裴波那契序列的定义为 f(0)=0, f(1)=0, ..., f(k-2)=0, f(k-1)=1; f(n)=f(n-1)+f(n-2)+...+f(n-k), n=k,k+1,... 试编写求k阶裴波那契序列的第m项值的函数算法，k和m均以值调用的形式在函数参数表中出现。

分析：
首先判断参数是否合理。用一个长度为k的数组作为临时存储区，将前k个数填入数组，也就是f(0), f(1), ... f(k-1)。之后根据题目定义的算法，下一个元素也就是当前数组中所有数的和。将这个数组看作是一个循环填入的数组，用得到的值替换掉当前的上一个填入位置的下一个位置。

```c
Status Fibonacci(int k, int m, int &f) 
/* 求k阶斐波那契序列的第m项的值f */
/* 否则（比如，参数k和m不合理）返回ERROR */
{
  int *a;
  a = (int*)malloc(k * sizeof(int)); 
  int left, count, sum = 0;
  int i, j;
  
  if (k < 2 || m < 0)
    return ERROR;
  for (i = 0; i < k - 1; i++) {
    a[i] = 0;
  }
  a[k - 1] = 1;
 
  if (m < k){
    f = a[m];
    return OK;
  }
  
  for (i = k; i <= m; i++) {
    left = i % k; 
    sum = 0;
    for (j = 0; j < k; j++) {
        sum += a[j];
    }  
    a[left] = sum;
  }  
  f = a[left];

  return OK;  
}
```
