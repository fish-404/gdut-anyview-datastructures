>【题目】编写算法，计算以邻接表方式存储的有向图G中k顶点的入度。图的邻接表存储结构的类型定义如下：
```c
#define UNVISITED  0
#define VISITED    1  
#define INFINITY MAXINT // 计算机允许的整数最大值，即∞
typedef char VexType;
typedef enum {DG,DN,UDG,UDN} GraphKind; // 有向图,有向网,无向图,无向网
typedef struct AdjVexNode {
  int adjvex;  // 邻接顶点在顶点数组中的位序
  struct AdjVexNode *next; // 指向下一个邻接顶点（下一条边或弧）
  int info;    // 存储边（弧）相关信息，对于非带权图可不用
} AdjVexNode, *AdjVexNodeP; // 邻接链表的结点类型
typedef struct VexNode {
  VexType data;    // 顶点值，VexType是顶点类型，由用户定义
  struct AdjVexNode *firstArc; // 邻接链表的头指针
} VexNode; // 顶点数组的元素类型
typedef struct {
  VexNode *vexs;  // 顶点数组，用于存储顶点信息
  int n, e;       // 顶点数和边（弧）数
  GraphKind kind; // 图的类型
  int *tags;      // 标志数组
} ALGraph;  // 邻接表类型
```

分析：

求顶点入度，需要遍历每个顶点的邻接链表，当邻接表中某个结点的存储位序等于k时，则可以提前结束该链表的查找，直至搜寻所有结点的邻接链表。

``` c++
int inDegree(ALGraph G, int k)
/* 求有向图G中k顶点的入度。若k顶点不存在，则返回-1 */
{
    AdjVexNodeP p;
    int count = 0;
    
    if (G.n <= 0)
        return -1;
    if (k < 0 || k > G.n)
        return -1;
    int i;
    for (i = 0; i < G.n; i++) {
        for (p = G.vexs[i].firstArc; p != NULL; p = p->next) {
            if (p->adjvex == k) {
                count++;
                continue;
            }            
        }
    } 
    return count;
}
```
