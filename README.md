# Infix-to-Postfix-and-postfix-evaluation
```
#include<stdio.h>
#include<stdlib.h>
#include<ctype.h>
#define n 10
int top=-1;
char infix[n],postfix[n];

//to check if stack is full
int isfull()
{
	if(top==n-1)
		return 1;
	else
		return 0;
}

//to check if stack is empty
int isempty()
{
	if(top==-1)
		return 1;
	else
		return 0;
}

//to insert element into stack
void push(int val)
{
	if(isfull())
		printf("\nOverflow");
	else
	{
		top++;
		stack[top]=val;
		printf("\n%d pushed",stack[top]);
	}
}

//to delete element from stack
void pop()
{
	if(isempty())
		printf("\nUnderflow");
	else
	{
		printf("\n%d popped",stack[top]);
		stack[top]=-1;
		top--;
	}
}

//to display elements
void display()
{
	if(isempty())
		printf("\nEmpty Stack");
	else
	{	
		printf("\nElements are: ");
		for(int i=top;i>=0;i--)
			printf("\n|%d| ",stack[i]);
		printf("\n```");
	}
}


int isoperator(char sym)
{
	if((sym=='+') || (sym=='-')
		return 1;
	else
		return 0;
}

int precedence(char sym)
{
	switch(sym)
	{
		case '*' : return 2;
		case '+' : return 1;
		default : return 0;
	}
}

void infixtopostfix()
{
	int i=0,j=0;
	char x,item;
	item=infix[i];
	while(item!='\0')
	{
		if((isdigit(item)||isalpha(item)))
		{
			postfix[j]=item;
			j++;
		}
		else if(isoperator(item))
		{
			x=topofstack()
			while((isoperator(x))&&(precedence(x)>=precedence(item)))
			{
				x=pop();
				postfix[j]=x;
				j++;
				x=topofstack();
			}
		}
		i++;
	}
	postfix[i]='\0';
}

void postfixeval()
{
	int i=0,val,n1,n2,n3,num;
	val=postfix[i];
	while(val!='\0')
	{
		if(isdigit(val))
		{
			num=atoi(val);
			push(num);
		}
		else
		{
			n1=pop();
			n2=pop();
			switch(val)
			{
				case '+' :
					n3=n1+n2;
					break;
				case '*' :
					n3=n1*n2;
					break;
			}
			push(n3);
		}
		i++;
		val=postfix[i];
	}
}
//pop result in main

void main()
{
	gets(infix);
	infixtopostfix();
	puts(postfix);
}
```
