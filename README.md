# C-
数据结构
#include <stdlib.h>  
#include <stdio.h>
#include<malloc.h>
#define LEN sizeof(NODE)
//定义链表数据结构
typedef int datatype;
typedef struct node
{
	datatype data;
	struct node*next;
} linknode, *link;
//函数声明
link Creatlist();
link Adjmax(link L1, int k);
main()
{
	int b = 0;
	link L = NULL, p3 = NULL;
	L = Creatlist();
	printf("请输入每组数据的个数k=");
	scanf("%d", &b);
	p3 = Adjmax(L, b);
	printf("第一个数为：%d\n", p3->data);
}

link Creatlist()
{
	int a;
	link P, r, H;                     //H, P, r分别表示表头，新节点和尾节点指针
	H = (link)malloc(sizeof(linknode));  //创建头节点
	r = H;
	printf("请按顺序输入链表的值,按enter键输入下一个数：\n");                   //输入一个数据
	while (	scanf("%d", &a))
	{
		P = (link)malloc(sizeof(linknode));//申请新的节点
		P->data = a;                      //存入数据
		r->next = P;                     //新节点链入表尾
		r = P;
	              //输入下一个数据
	}
	fflush(stdin) ;
	r->next = NULL;//将尾节点置空
	return(H);//返回已创建好的头节点
}

link Adjmax(link L1, int k)//求相邻k个节点之间data值之和最大的第一节点界定的算法
{
	link p, p1,p2 ,p4,q;
	int m0 = 0, m1 = 0,t=1, i;

	p = p1 = L1->next;
	if (p1 == NULL)return(p1);//表空返回
	q = p;
	p2=p;
	p4=p;//初始化p,p1,p2,p4,q
	 
   
   for (i = 0; i < k; i++)
	{
	
		if (p1 == NULL)return(q);//表长为小于k时返回头节点 
	    m0 += p1->data;
		p1 = p1->next;
	}
    
    printf("第一组数据的和：%d\n",m0) ;
    
    while (p1)
	{
	
	    p2=p2->next;	//p2记录每组数据的第一位 
	    
	    p1=p2 ;         //p1获取第一个位置，开始位移 
		
		 
		m1=0;//每次循环清空m0 
   
	    	for (i = 0; i < k; i++)
		    {   
	       	if (p1 == NULL) {m1=0;i=k;}
	     	else {m1 += p1->data;p1=p1->next; }
            
		    }
		   
		 if (m1 > m0)
		  { m0 = m1;q=p2 ;}//找到最大的和之后，将该组数据的第一位传给q 

    }
      
        printf("最大一组数据的和：%d\n",m0) ;
  while(p4!=q)//查找q所在的序号 
	{   t++;
     	p4=p4->next;
     	
	}
       
        printf("第一个数的序号：%d\n",t) ;
		return (q);//返回这组数据的第一个节点 
}
