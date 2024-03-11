 
#include<stdio.h> 

#include<ctype.h> 

#include<string.h> 

int main() 

{ 

FILE *input, *output; 

int l=1; 

int t=0; 

int j=0; 

int i,flag; 

char ch,str[20]; 

input = fopen("input.txt","r"); 

output = fopen("output.txt","w"); 

char keyword[30][30] = {"int","main","if","else","do","while"}; 

fprintf(output,"Line no. \t Token no. \t Token \t Lexeme\n\n"); 

while(!feof(input)) 

{ 

i=0; 

flag=0; 

ch=fgetc(input); 

if( ch=='+' || ch== '-' || ch=='*' || ch=='/' ) 

{ 

fprintf(output,"%7d\t\t %7d\t\t Operator\t %7c\n",l,t,ch); 

t++; 

} 

else if( ch==';' || ch=='{' || ch=='}' || ch=='(' || ch==')' || ch=='?' || 

ch=='@' || ch=='!' || 

ch=='%') 

{ 

fprintf(output,"%7d\t\t %7d\t\t Special symbol\t %7c\n",l,t,ch); 

t++; 

} 

 

else if(isdigit(ch)) 

{ 

fprintf(output,"%7d\t\t %7d\t\t Digit\t\t %7c\n",l,t,ch); 

t++; 

} 

else if(isalpha(ch)) 

{ 

str[i]=ch; 

i++; 

ch=fgetc(input); 

while(isalnum(ch) && ch!=' ') 

{ 

str[i]=ch; 

i++; 

ch=fgetc(input); 

} 

str[i]='\0'; 

for(j=0;j<=30;j++) 

{ 

if(strcmp(str,keyword[j])==0) 

{ 

flag=1; 

break; 

} 

} 

if(flag==1) 

{ 

fprintf(output,"%7d\t\t %7d\t\t Keyword\t %7s\n",l,t,str); 

t++; 

} 

else 

{ 

fprintf(output,"%7d\t\t %7d\t\t Identifier\t %7s\n",l,t,str); 

t++; 

} 

 

} 

else if(ch=='\n') 

{ 

l++; 

} 

} 

fclose(input); 

fclose(output); 

return 0; 

} 
#include<stdio.h> 

void main() 

{ 

printf("Hello World"); 

}  

 output: 

 	Line no. Token no. Token Lexeme 

1 0 Identifier include 

1 1 Identifier stdio 

1 2 Identifier h 2 3 Identifier void 

2 4 Keyword main 

2 5 Special symbol ) 

3 6 Special symbol { 

4 7 Identifier printf 

4 8 Identifier Hello 

4 9 Identifier World 

4 10 Special symbol ) 

4 11 Special symbol ; 

5 12 Special symbol } 
############second program########################
################################################################################
#include<stdio.h> #include<conio.h> #include<string.h> #include<stdlib.h> void main()

{

//e,e'=E,t,t'=T

char input[7]="i+i*i$",m[6][7][9]={" ","+","*","(",")","i","$",

"e","_","_","e->tE","_","e->tE","_",

"E","E->+tE","_","_","E->@","_","E->@",

"t","_","_","t->fT","_","t->fT","_",

"T","T->@","T->*fT","_","T->@","_","_",

"f","_","_","f->(e)","_","f->i","_"};

char stack[20],x,a,prod[6];

int i,j,k,inp=0,top=0,xp,ap,max=6; stack[0]='$';

clrscr();

printf("Predictive Parser\n"); printf("\nStack\tInput\n"); printf(" "); top++;

stack[top]='e'; do

{

a=input[inp]; x=stack[top]; if(x==a)

{

printf("\n"); for(i=0;i<top;i++) printf("%c",stack[i]); printf("\t%s",input); stack[top]=' ';

input[inp]=' '; top--;

inp++;

}

else

{

//finding positions for(i=0;i<7;i++) if(m[0][i][0]==a)

{

ap=i; break;

}

for(i=0;i<6;i++) if(m[i][0][0]==x)

{

xp=i; break;

}

// reading entry from parsing table if(m[xp][ap][0]==' ')

{

printf("error"); exit(1);

}

else

{

for(i=0,k=3;k<8;k++,i++)

{

prod[i]=m[xp][ap][k];

}

strrev(prod);

}

//stack operations if(prod[0]=='@')

{

printf("\n"); for(i=0;i<=top;i++) printf("%c",stack[i]); printf("\t%s",input); stack[top]=' ';

top--;

}

else

{

printf("\n"); for(i=0;i<=top;i++) printf("%c",stack[i]); printf("\t%s",input);

//pop stack[top]=' '; top--;

//push for(i=0;i<strlen(prod);i++)

{

top++; stack[top]=prod[i];

}

}

}

}

while(stack[top]!='$');

if(stack[top]=='$'&&input[inp]=='$')

{

printf("\n%c\t\ %c\nString is accepted",stack[top],input[inp]);

}

else

{

printf("not accepted");

}

getch();

}
