```c
#include <stdio.h>
#include <stdlib.h>


void prin(const char* title, double pt[3][4][3], int a, int b, int c) {
	printf("\nPrintint %s array\n", title);
	for (int i = 0; i < a; i++)
	{
		printf("[ ");
		for (int j = 0; j < b; j++)
		{
			printf("{");

			for (int k = 0; k < c; k++)
				printf("%3.0f", pt[i][j][k]);

			printf("}");
			if (j != b - 1) printf(", ");
		}
		printf(" ]\n");
	}
}

int main()
{
	double a[3][4][3] =
	{
		{ {1,2,3},{4,5,6},{7,8,9},{10,11,12} },
		{ {13,14,15},{16,17,18},{19,20,21} ,{22,23,24} },
		{ {25,26,27},{28,29,30},{31,32,33} ,{34,35,36} }
	};

	prin("a", a, 3, 4, 3);

	double(*b)[4][3];
	b = (double(*)[4][3])malloc(sizeof(double[3][4][3]));

	b = a;
	prin("b", b, 3, 4, 3);

	double* (*c)[4];
	c = (double* (*)[4]) malloc(sizeof(double* [4][3]));
	//c = a;
	for (int i = 0; i < 3; i++)
		for (int j = 0; j < 4; j++)
		c[i][j] = b[i][j];

	printf("%d\n",sizeof(c));
	printf("%d\n",sizeof(a));
	printf("%d\n",sizeof(b));


	//printf("\n");
	/*printf("%p\n",a);
	printf("%p\n",b);
	printf("%p\n",c);
	printf("%p\n",*(*c));
	printf("%p\n",**c);*/
	printf("%p\n", *(*c+1));
	printf("%p\n", *(*(c+1)+1));

	

	for (int i = 0; i < 3; i++) 
	{
		for (int j = 0; j < 4; j++) 
		{
			for (int k = 0; k < 3; k++) 
				printf("%p ", &a[i][j][k]);
			printf("\n");
		}
		printf("\n");
	}
	for (int i = 0; i < 3; i++)
	{
		for (int j = 0; j < 4; j++)
		{
			for (int k = 0; k < 3; k++)
				printf("%lf ", c[i][j][k]);
			printf("\n");
		}
		printf("\n");
	}

	prin("c", **c, 3, 4, 3);

	return 0;
}
```

