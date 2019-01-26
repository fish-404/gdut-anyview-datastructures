>【题目】编写递归算法，计算二叉树T中叶子结点的数目。二叉链表类型定义：
```c
typedef struct BiTNode {
  TElemType  data;
  struct BiTNode  *lchild, *rchild;
} BiTNode, *BiTree;
```
分析：

若果该结点为叶子结点，即没有左子树和右子树，返回计数值1

若果非叶子结点，则对该结点递归求解

结点总数为左子树上的叶子结点加上右子树上的叶子结点

```c
int Leaves(BiTree T)
/* 计算二叉树T中叶子结点的数目 */
{
    if (T == NULL)
        return ERROR;
    if (NULL == T->lchild && NULL == T->rchild)
        return 1;
    return Leaves(T->lchild) + Leaves(T->rchild);
}
```
