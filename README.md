
#include<iostream>
using namespace std;

void swap(int* x,int* y)
{
	int tmp = *x;
	*x = *y;
	*y = tmp;
}
int partition(int data[],int length ,int start ,int end)
{
	if(data == NULL || length <= 0|| start < 0|| end >= length )
	{
		printf("参数传递错误:data == NULL || length <= 0|| start < 0|| end >= length \n");
		return -1;
	}

	int index =( start + end )/2;
	swap( &data[index], &data[end] );

	int small = start -1;
	for(index = start ;index <end ;++index )
	{
		if(data[index]<data[end])
		{
				++small;
		
			if(small != index)
				swap(&data[small],&data[index]);
	    }
	}
	++ small;
	swap(&data[small], &data[end] );

	return small;
}
void quicksort(int data[],int length ,int start, int end)
{
	//if(data == NULL || length <= 0|| start < 0|| end >= length )
	//{
	//	printf("参数传递错误:data == NULL || length <= 0|| start < 0|| end >= length \n");
	//	return ;
	//}
	if(start == end )
	{
		return ;
	}
	int index = partition(data,length,start,end);
	if(index >start )
	{
		quicksort(data, length, start,index-1 );
	}
	if(index < end )
	{
		quicksort(data, length,index+1,end );
	}
}
//===================================测试代码=======================================
void test()
{
	int data[100] = {20,30,404,35,92,34,16,97,55,44,22,4,32,442,65,234,22,20, 365,202,
	                 10,40,454,32,22,4,166,87,55,44,282,404,892,442,65,234,22,210, 3655,2021,
	                 20,110,414,36,2,34,166,77,55,44,822,4444,2,442,65,234,992,220, 3665,2022,
	                 30,120,424,37,22,34,166,7,55,44,228,46,72,442,65,234,222,230, 3675,2023,
					20,30,414,32,22,34,166,67,5,644,229,48,42,4422,65,234,232,240, 3685,2024};

	int length = sizeof(data)/sizeof(data[0]);
	int start = 0;
	int end = length - 1 ;
	printf("总共需要对%d个数字进行排序\n",length);
	quicksort(data, length , start,  end);

	for(int i = 0; i< length ; ++i )
	{
		printf("%4d ",data[i]);
	}
	printf("\n");
}

int main()
{
	test();
	return 0;
}
