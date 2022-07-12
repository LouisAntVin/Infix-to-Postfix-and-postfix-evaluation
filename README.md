# Infix to Postfix
```
#include<stdio.h>
#include<stdlib.h>
#include<ctype.h>
int top=-1;
char stack[100];

//to insert element into stack
char push(char val)
{
	stack[++top]=val;
	
}

//to delete element from stack
char pop()
{
	if(top == -1)
        return -1;
    else
        return stack[top--];
}

//to display elements
void display()
{
	for(int i=top;i>=0;i--)
		printf("\n%d ",stack[i]);
}

/*
int isoperator(char sym)
{
	if((sym=='+') || (sym=='-') || (sym=='*') || (sym=='/') || (sym=='('))
		return 1;
	else
		return 0;
}
*/
int precedence(char sym)
{
	switch(sym)
	{
		case  '(' : return 0;
		case '*' : return 1;
		case  '/' : return 1;
		case '+' : return 2;
		case '-' : return 2;
		default : return 0;
	}
}

void main()
{
	int i=0;
	char item,x,in[100];
	printf("Enter the expression : ");
    scanf("%s",in);
	while(in[i]!='\0')
	{
		item=in[i];
		if(isalnum(item))
			printf("%c ",item);
        else if(item == '(')
            push(item);
        else if(item == ')')
        {
            while((x = pop()) != '(')
                printf("%c ",x);
        }
        else
        {
            while(precedence(stack[top]) >= precedence(item))
                printf("%c ",pop());
            push(item);
        }
        i++;
    }
    while(top != -1)
    {
        printf("%c ",pop());
    }
    printf("\n");
}
```
# Postfix evaluation
```
#include<stdio.h>
#include<ctype.h>
int stack[20];
int top = -1;

void push(int x)
{
    stack[++top] = x;
}

int pop()
{
    return stack[top--];
}

void main()
{
    char px[20];
    int n1,n2,n3,num,i=0;
    printf("Enter the expression : ");
    scanf("%s",px);
    while(px[i] != '\0')
    {
        if(isdigit(px[i]))
        {
            num = px[i] - 48;
            push(num);
        }
        else
        {
            n1 = pop();
            n2 = pop();
            switch(px[i])
            {
		        case '+':
		        {
		            n3 = n1 + n2;
		            break;
		        }
		        case '-':
		        {
		            n3 = n2 - n1;
		            break;
		        }
		        case '*':
		        {
		            n3 = n1 * n2;
		            break;
		        }
		        case '/':
		        {
		            n3 = n2 / n1;
		            break;
		        }
           }
            push(n3);
        }
        i++;
    }
    printf("\nThe result of the expression %s  =  %d\n\n",px,pop());
}
```
