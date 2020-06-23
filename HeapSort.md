#include <stdio.h>
#include <stdlib.h>
/*这个运用了完全二叉树的原理，采用大顶堆把最大的推到根，再放到最后,再把
剩下n-1个做成大顶堆，再把最大的放到最后，以此类推
完全二叉树的一个性质：编号为i的节点左右子树为2*i和2*i+1*/
typedef struct Node
{
    int *r;
    int length;
}Node;

Node Init(Node L, int n);
Node HeapSort(Node L);
Node HeapAdjust(Node L,int s,int n);
Node swap(Node L,int a,int b);


int main()
{
    int i,n;
    Node L;
    scanf("%d",&n);
    L = Init(L,n);
    for(i=1;i<=n;i++)
        scanf("%d",&L.r[i]);

    L = HeapSort( L );

    for(i=1;i<=n;i++)
        printf("%d ",L.r[i]);
    printf("\n");
    return 0;
}

Node Init(Node L , int n)
{
    L.length = n;
    L.r = (int *)malloc(sizeof(int)*(n+1));
    return L;
}

Node HeapSort(Node L)
{
    int i;

    for(i=L.length/2 ;i>0; i--)//从最低层的非叶节点开始往上走，
    {
        L = HeapAdjust(L,i,L.length);
        //先对整体所有节点进行与孩子的堆排
    }

    for(i=L.length; i>1; i--)
    {
        L = swap(L,1,i);//最大的从第一个转到最后一个
        L = HeapAdjust(L,1,i-1);//再把前n-1个进行堆排
    }
    return L;
}

Node HeapAdjust(Node L,int s,int n)
{
    int i,temp;
    temp = L.r[s];

    for(i=2*s; i<=n; i*=2)
    {
        if(i<n && L.r[i]<L.r[i+1])//右叶子比左叶子大，转到右叶子
        {
            i++;
        }

        if(temp >= L.r[i])//如果没有双亲大那就返回了，否则就换值再往下比
            break;
        L.r[s] = L.r[i];
        s = i;
    }

    L.r[s] = temp;
    return L;
}

Node swap(Node L,int a,int b)
{
    int temp;
    temp = L.r[a];
    L.r[a] = L.r[b];
    L.r[b] = temp;
    return L;
}
