#include<stdio.h>
#include<stdlib.h>
//直插+希尔，希尔就是进行多次直插来增强有序性，最后来一次直插
typedef struct Node
{
    int *r;
    int length;
}Node;

Node ShellSort( Node L );
Node InsertSort( Node L );
Node Init(Node L, int n);

int main()
{
    int i,n;
    Node L;
    scanf("%d",&n);
    L = Init(L,n);
    for(i=0;i<n;i++)
        scanf("%d",&L.r[i]);

    L = ShellSort( L );

    for(i=0;i<n;i++)
        printf("%d ",L.r[i]);
    printf("\n");
    return 0;
}

Node Init(Node L , int n)
{
    L.length = n;
    L.r = (int *)malloc(sizeof(int)*n);
    return L;
}

Node InsertSort(Node L)
{
    int i,j,temp ;
    for(i=0;i<L.length-1;i++)
    {
        if(L.r[i]>L.r[i+1])
        {
            temp = L.r[i+1];
            for(j=i;L.r[j]>temp && j!=-1;j--)
            {
                L.r[j+1] = L.r[j];
            }
            L.r[j+1] = temp;
        }
    }
    return L;
}

Node ShellSort(Node L)
{
    int i,j,k,temp ,gap;
    for(gap=L.length/2;gap>=1;gap/=2) //每次以一半为步长
    {
        for(i=0;i<gap;i++)
        {
            for(k=i;k+gap<L.length;k+=gap)
            {
                temp = L.r[k+gap];
                for(j=k;L.r[j]>temp && j>=0;j-=gap)
                {
                    L.r[j+gap] = L.r[j];
                }
                L.r[j+gap] = temp;
            }
        }
    }
    return L;
}
