>【题目】编写递归算法：求二叉树中以元素值为x的结点为根的子树的深度。二叉链表类型定义：
``` c
typedef struct BiTNode {
  TElemType data;
  struct BiTNode  *lchild, *rchild;
} BiTNode, *BiTree;
```
分析： 
1. 判断是否为空树，若为空树，深度为0；
2. 判断数据域是否为x，若为x，左右子树深度较大的加一即为所求深度；
3. 若数据域不为x，则递归对左右子树求解Depthx。
``` c
int Depthx(BiTree T, TElemType x)
/* 求二叉树中以值为x的结点为根的子树深度 */
{
    int depl, depr;
    
    if (T == NULL)
        return 0;
    
    if (T->data == x) {
        depl = Depthx(T->lchild, T->lchild->data) + 1;
        depr = Depthx(T->rchild, T->rchild->data) + 1;
        
        return depl > depr ? depl : depr;
    }
    else {
        depl = Depthx(T->lchild, x);
        depr = Depthx(T->rchild, x);
        if (depl == 0 && depr != 0) 
            return depr;
        else if (depl != 0 && depr == 0) 
            return depl;
        else if (depl == 0 && depr == 0)
            return 0;
    }    
}
```
