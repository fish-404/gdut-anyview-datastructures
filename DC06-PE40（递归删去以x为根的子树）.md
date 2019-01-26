>【题目】编写递归算法：对于二叉树中每一个元素值为x的结点，删去以它为根的子树，并释放相应的空间。二叉链表类型定义：
``` c
typedef struct BiTNode {
  TElemType data;
  struct BiTNode  *lchild, *rchild;
} BiTNode, *BiTree;
```
分析：
1. 判断树是否非空；
2. 判断数据域是否等于x，若是，递归删去分别以该树的左右子树的根节点的值域作为x的子树；
3. 若否，将待查找树改为该树的左右子树。
``` c++
void ReleaseX(BiTree &T, char x)
/* 对于二叉树T中每一个元素值为x的结点， */
/* 删去以它为根的子树，并释放相应的空间 */
{
    if (T != NULL) {
        if (T->data == x) {
            ReleaseX(T->lchild, T->lchild->data);
            ReleaseX(T->rchild, T->rchild->data);
            free(T->lchild);
            free(T->rchild);
            free(T);
        }
        else {
            ReleaseX(T->lchild, x);
            ReleaseX(T->rchild, x);
        }
    }
}
```
