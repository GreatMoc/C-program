#include <stdio.h>
#include <stdlib.h>
//快排，用递归，来回拉扯
typedef struct Node
{
    int *r;
    int length;
}Node;


Node QuickSort(Node L);
Node QSort(Node L,int low,int high);
Node change(Node L,int low, int high);
Node partition(Node L, int low,int high,int *point);


Node Init(Node L , int n)
{
    L.length = n;
    L.r = (int *)malloc(sizeof(int)*n);
    return L;
}

int main()
{
    int i,n;
    Node L;
    scanf("%d",&n);
    L = Init(L,n);
    for(i=0;i<n;i++)
        scanf("%d",&L.r[i]);

    L = QuickSort( L );

    for(i=0;i<n;i++)
        printf("%d ",L.r[i]);
    printf("\n");
    return 0;
}

Node QuickSort(Node L)
{
    L = QSort(L,0,L.length-1);
    return L;
}

Node change(Node L,int low, int high)//交换
{
    int temp;
    temp = L.r[low];
    L.r[low] = L.r[high];
    L.r[high] = temp;
    return L;
}
Node partition(Node L, int low,int high,int *point)
//在这里把创建的基准点两侧的的都排好，然后返回这个基准点
{
    *point = L.r[low];

    while(low<high)
    {
        while(low<high && L.r[high] >= *point)
        {
            high--;
        }
        L = change(L,low,high);
        while(low<high && L.r[low] <= *point)
        {
            low++;
        }
        L = change(L,low,high);
    }
    *point = low;
    return L;
}

Node QSort(Node L, int low, int high)
{
    int point;

    if(low < high)//递归条件
    {
        L = partition(L,low,high,&point);//找基准点

        QSort(L,low,point-1);

        QSort(L,point+1,high);
    }
    return L;
}
