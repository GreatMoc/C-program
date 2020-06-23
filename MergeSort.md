#include <stdio.h>
#include <stdlib.h>
//并桂排序的递归做法，序列先拆，最后再合;以及迭代算法，解释挺全的
typedef struct Node
{
    int *r;
    int length;
}Node;

Node MergeSort( Node L ,int n);
Node Init(Node L, int n);
Node Merging(Node list1,int list1_size,Node list2,int list2_size);

int main()
{
    int i,n;
    Node L;
    scanf("%d",&n);
    L = Init(L,n);
    for(i=0;i<n;i++)
        scanf("%d",&L.r[i]);

    L = MergeSort(L,n);

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

Node MergeSort( Node L ,int n)//递归实现
{
    if(n>1)
    {
        Node list1,list2;//左边，右边一人一边
        list1.r = L.r;
        list2.r = L.r +n/2;
        int list1_size=n/2 , list2_size=n-list1_size;//两边的长度分好
        //分别把左右递归排序
        list1 = MergeSort(list1, list1_size);
        list2 = MergeSort(list2, list2_size);
        //左右结合排序
        L = Merging(list1,list1_size,list2,list2_size);
    }
    return L;//返回上一级

}

Node Merging(Node list1,int list1_size,Node list2,int list2_size)//归并过程
{    //这里就是把两个序列结合，不用多说了
    int i,j,k;
    Node temp;
    temp = Init(temp , list1_size+list2_size);
    i=j=k=0;
    while(i<list1_size && j<list2_size)
    {
        if(list1.r[i]<list2.r[j])
            temp.r[k++] = list1.r[i++];
        else
            temp.r[k++] = list2.r[j++];
    }
    while(i<list1_size)
        temp.r[k++] = list1.r[i++];
    while(j<list2_size)
        temp.r[k++] = list2.r[j++];
    return temp;
}

/*Node MergeSort(Node L,int n)
{
    int i,left_min, left_max,right_min, right_max,next;
    Node temp;
    temp = Init(temp,n);

    for(i=1; i<n; i*=2)//控制步长数，从小一点点变大
    {
        for(left_min=0; left_min<n-i; left_min = right_max)//每个步长下的一趟
        {
            right_min = left_max = left_min+i;
            right_max = left_max+i;

            if(right_max > n)
                right_max = n;//仿制超数

            next = 0;
            while( left_min<left_max && right_min<right_max)
            {
                if( L.r[left_min]<L.r[right_min])
                    temp.r[next++] = L.r[left_min++];
                else
                    temp.r[next++] = L.r[right_min++];
            }

            while(left_min < left_max) //出现右边排完左边没拍完的情况
                L.r[--right_min] = L.r[--left_max];
            while(next>0)
                L.r[--right_min] = temp.r[--next];
        }
    }
    return L;
}
*/
