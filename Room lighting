#include<reg51.h>
#define lcd P1
sbit rs=P3^6;
sbit e=P3^7;
sbit relay=P0^0;
sbit s1=P2^0;
sbit s2=P2^1;
void delay (int);
void cmd (char);
void display (char);
void init (void);
void string (char *);
void view (int);
int count=0;
int no[10]={48,49,50,51,52,53,54,55,56,57};
void delay (int d)
{
	unsigned char i=0;
	for(;d>0;d--)
	{
		for(i=250;i>0;i--);
		for(i=248;i>0;i--);
	}
}
void cmd (char c)
{
	lcd=c;
	rs=0;
	e=1;
	delay(5);
	e=0;
}
void display (char c)
{
	lcd=c;
	rs=1;
	e=1;
	delay(5);
	e=0;
}
void string (char *p)
{
	while(*p)
	{
		display(*p++);
	}
}
void view (int n)
{
	cmd(0xc0);
	display(no[(n/10)%10]);
	display(no[n%10]);
}
void init (void)
{
	cmd(0x38);
	cmd(0x0c);
	cmd(0x01);
	cmd(0x80);
}
void main()
{
  init();
	string("counter........");
	cmd(0xc0);
	
	view(count);
	
	
	while(1)
	{
		if(s1==1)
		{
			while(s2==0);
			if(count!=99)
			count=count+1;
			while(s2==1); 
			view(count);
		}
		else if(s2==1)
		{
			while(s1==0);
			if(count!=0)
			count=count-1;
			while(s1==1);
			view(count);
		}
		else if(count==1)
			relay=0;
		else if(count==0)
			relay=1;
		
	}
}
