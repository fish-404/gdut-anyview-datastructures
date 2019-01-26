>【题目】试写一算法，在带头结点单链表删除第i元素到e。
带头结点单链表的类型定义为：
```c
typedef struct LNode {
  ElemType      data;
  struct LNode *next;
} LNode, *LinkList;
```

**分析**：
要删除第i个元素，需要找到该元素所在结点。定义一个结点指针通过循环来寻找该结点，但如果直接找到的是该结点，则在删除时无法找到前一个结点，因此应该去寻找要删除的结点的前一个结点。定义一个变量来记录当前处于第几个结点，与给定值i进行比较，当到达该结点的前一个结点时，停止循环。取出下一个结点的元素，并删除下一个结点。

需要注意的是
若i的数值恰好比该链表长度大1，已经超出了长度，需要报错。
头结点不含数据，因此`i=0`时也属于参数不合法的情况。   
```c++
Status Delete_L(LinkList L, int i, ElemType &e)
/* 在带头结点单链表L删除第i元素到e，并返回OK。*/
/* 若参数不合理，则返回ERROR。                */
{
    LNode *p;
    int j = 0;
    
    if (i <= 0) 
        return ERROR;
    
    p = L;
    
    while (j < i - 1) {
        if (p->next != NULL) {        
            p = p->next;
            j++;      
        }
        else
            return ERROR;
    }
    if (p->next == NULL)
        return ERROR;
        
    e = p->next->data;
    p->next = p->next->next;
     
    return OK;    
}
```
