>【题目】试对一元稀疏多项式Pn(x)采用存储量同多项式项数m成正比的顺序存储结构，编写求Pn(x0)的算法（x0为给定值）。一元稀疏多项式的顺序存储结构:
``` c
typedef struct {
  int  coef;  // 系数
  int   exp;  // 指数
} Term;

typedef struct {
  Term  *elem;   // 存储空间基址
  int    length; // 长度（项数）
} Poly;
```
``` c
float Evaluate(Poly P, float x)
/* P.elem[i].coef 存放ai，                        */
/* P.elem[i].exp存放ei (i=1,2,...,m)              */
/* 本算法计算并返回多项式的值。不判别溢出。       */
/* 入口时要求0≤e1<e2<...<em，算法内不对此再作验证 */
{
    int i, j;
    float value = 0, temp;
    
    for (i = 0; i < P.length; i++) {
        temp = 1;
        j = P.elem[i].exp;
        for (; j > 0; j--) {
            temp *= x;
        }
        value += P.elem[i].coef * temp;
    }
    
    return value;
}
```
