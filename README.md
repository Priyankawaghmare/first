
#include<iostream>
#include<stdlib.h>
using namespace std;

void create();  // For creating a graph
void dfs();  // For Deapth First Search(DFS) Traversal.
void bfs();  // For Breadth First Search(BFS) Traversal.

struct node  // Structure for elements in the graph
{
   int data,status;
   struct node *next;
   struct link *adj;
};

struct link  // Structure for adjacency list
{
   struct node *next;
   struct link *adj;
};

struct node *start,*p,*q;
struct link *l,*k;

int main()
{
   int choice;

   create();
   while(1)
   {
      cout<<"-----------------------";
      cout<<"\n1: DFS \n2: BSF\n3: Exit\nEnter your choice: ";
      cin>>choice;
      switch(choice)
      {
	 case 1:
	    dfs();
	    break;
	 case 2:
	    bfs();
	    break;
	 case 3:
	    exit(0);
	    break;
	 default:
	    cout<<"Incorrect choice!Re-enter your choice.";

      }
   }
   return 0;
}

void create()    // Creating a graph
{
   int dat,flag=0;
   start=NULL;
   cout<<"Enter the nodes in the graph(0 to end): ";
   while(1)
   {
      cin>>dat;
      if(dat==0)
	 break;
      p=new node;
      p->data=dat;
      p->status=0;
      p->next=NULL;
      p->adj=NULL;
      if(flag==0)
      {
	 start=p;
	 q=p;
	 flag++;
      }
      else
      {
	 q->next=p;
	 q=p;
      }
   }
   p=start;
   while(p!=NULL)
   {
      cout<<"Enter the links to "<<p->data<<" (0 to end) : ";
      flag=0;
      while(1)
      {
	 cin>>dat;
	 if(dat==0)
	    break;
	 k=new link;
	 k->adj=NULL;
	 if(flag==0)
	 {
	    p->adj=k;
	    l=k;
	    flag++;
	 }
	 else
	 {
	    l->adj=k;
	    l=k;
	 }
	 q=start;
	 while(q!=NULL)
	 {
	    if(q->data==dat)
	       k->next=q;
	    q=q->next;
	 }
      }
      p=p->next;
   }
   cout<<"-------------------------";
   return ;
}


void bfs()
{
   int qu[20],i=1,j=0;
   p=start;
   while(p!=NULL)
   {
      p->status=0;
      p=p->next;
   }
   p=start;
   qu[0]=p->data;
   p->status=1;
   while(1)
   {
      if(qu[j]==0)
	 break;
      p=start;
      while(p!=NULL)
      {
	 if(p->data==qu[j])
	     break;
	 p=p->next;
      }
      k=p->adj;
      while(k!=NULL)
      {
	 q=k->next;
	 if(q->status==0)
	 {
	    qu[i]=q->data;
	    q->status=1;
	    qu[i+1]=0;
	    i++;
	 }
	 k=k->adj;
      }
      j++;
   }
   j=0;
   cout<<"Breadth First Search Results";
   cout<<"---------------------------";
   while(qu[j]!=0)
   {
      cout<<qu[j]<<"  ";
      j++;
   }

   return;
}

void dfs()
{
   int stack[25],top=1;
   cout<<"Depth First Search Results";
   cout<<"---------------------------";
   p=start;
   while(p!=NULL)
   {
      p->status=0;
      p=p->next;
   }
   p=start;
   stack[0]=0;
   stack[top]=p->data;
   p->status=1;
   while(1)
   {
      if(stack[top]==0)
	 break;
      p=start;
      while(p!=NULL)
      {
	 if(p->data==stack[top])
	    break;
	 p=p->next;
      }
      cout<<stack[top]<<"  ";
      top--;
      k=p->adj;
      while(k!=NULL)
      {
	 q=k->next;
	 if(q->status==0)
	 {
	    top++;
	    stack[top]=q->data;
	    q->status=1;
	 }
	 k=k->adj;
      }
   }

   return;
}
________________________________________
output:-


Enter the nodes in the graph(0 to end): 1
2
3
4
5
0
Enter the links to 1 (0 to end) : 2
3
4
0
Enter the links to 2 (0 to end) : 1 3 5 0
Enter the links to 3 (0 to end) : 2 4 0
Enter the links to 4 (0 to end) : 1 5 3 0
Enter the links to 5 (0 to end) : 2 0
------------------------------------------------
1: DFS 
2: BSF
3: Exit
Enter your choice: 1
Depth First Search Results---------------------------1  4  5  3  2  -----------------------
1: DFS 
2: BSF
3: Exit
Enter your choice: 2
Breadth First Search Results---------------------------1  2  3  4  5  -----------------------
1: DFS 
2: BSF
3: Exit
Enter your choice: 4
Incorrect choice!Re-enter your choice.-----------------------
1: DFS 
2: BSF
3: Exit
Enter your choice: 3
