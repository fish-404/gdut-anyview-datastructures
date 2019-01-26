>【题目】试写一算法，在带头结点单链表删除第i元素起的所有元素。带头结点单链表的类型定义为：
```c
typedef struct LNode {
  ElemType      data;
  struct LNode *next;
} LNode, *LinkList;
```
分析：
找到第i-1个结点的方法和PE84方法相同，找到该结点后，为了删除后面的所有元素，只需要将该结点的下一个结点置为空即可。
```C++
Status Cut_L(LinkList L, int i)
/* 在带头结点单链表L删除第i元素起的所有元素，并返回OK。*/
/* 若参数不合理，则返回ERROR。                         */
{
    LNode *p;
    int j = 0;
    
    p = L;
    if (i <= 0)
        return ERROR;
        
    while (j < i - 1) {
        if (p->next == NULL)
            return ERROR;
        p = p->next;
        j++; 
    }
    
    if (p->next == NULL)
        return ERROR;
        
    p->next = NULL;
    
    return OK;
}
```
