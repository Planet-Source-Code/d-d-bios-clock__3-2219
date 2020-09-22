<div align="center">

## Bios Clock


</div>

### Description

It shows your computer's BIOS time. Make sure you don't run it on Windows 2000, becasue Windows 2000 does not fully support BGI in Dos.
 
### More Info
 
Sends Minutes, hours, and seconds to the bios function.

Make sure you don't run it on Windows 2000, becasue Windows 2000 does not fully support BGI in Dos.

returns the current time.


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[D/D\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/d-d.md)
**Level**          |Intermediate
**User Rating**    |5.0 (10 globes from 2 users)
**Compatibility**  |C, C\+\+ \(general\), Borland C\+\+, UNIX C\+\+
**Category**       |[Complete Applications](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/complete-applications__3-7.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/d-d-bios-clock__3-2219/archive/master.zip)

### API Declarations

```
#include <graphics.h>
#include <stdlib.h>
#include <stdio.h>
#include <conio.h>
#include <dos.h>
#include <math.h>
#include <string.h>
```


### Source Code

```
#define PI 3.14152692
void second_hand(int midx,int midy,int d);
void min_hand(int midx,int midy,int d);
void hour_hand(int midx, int midy,int d);
int xc, yc, radius=150, charsize=2,d;  //radius of the circle
char buffer[80];
void digitxy(int d);
 int midx, midy;
void mainpage(void);
  struct time t;
int main(void)
{
  int gdriver = DETECT, gmode, errorcode,color;
  initgraph(&gdriver, &gmode, "c:\\bc5\\bgi");
  errorcode = graphresult();
  if (errorcode != grOk)
  {
  printf("Graphics error: %s\n", grapherrormsg(errorcode));
  printf("Press any key to halt:");
  getch();
  exit(1);
  }
  midx = getmaxx() / 2;
  midy = getmaxy() / 2;
  xc=midx;
  yc=midy;
  circle(midx, midy, radius);
  for(d=5;d<=60;d+=5)
   digitxy(d);
  do{
   gettime(&t);
   second_hand(midx,midy,t.ti_sec);
   min_hand(midx,midy,t.ti_min);
   hour_hand(midx,midy,t.ti_hour);
 	 delay(1000);
   floodfill(midx,midy,15);
  }while(!kbhit());
  getch();
  closegraph();
}
void digitxy(int d)
{
  int dx = (int) (cos((d/60.0)*2.*PI-PI/2.)*140+xc);
  int dy = (int) (sin((d/60.0)*2.*PI-PI/2.)*140+yc);
	sprintf(buffer,"%d",d/5);
  outtextxy(dx,dy,buffer);
  setcolor(WHITE);
}
void second_hand(int midx,int midy,int d)
{
  int dx = (int) (cos((d/60.0)*2.*PI-PI/2.)*140+xc);
  int dy = (int) (sin((d/60.0)*2.*PI-PI/2.)*140+yc);
  if(dy - yc >= 0)
  	dy+=charsize;
  else
  	dy-=charsize/2;
  if(dx -xc >=0)
  	dx+=charsize/2;
  else
setfillstyle(1,4);
 dx-=charsize;
 moveto(midx,midy);
 lineto(dx,dy);
 setcolor(YELLOW);
}
void min_hand(int midx,int midy,int d)
{
  int dx = (int) (cos((d/60.0)*2.*PI-PI/2.)*120+xc);
  int dy = (int) (sin((d/60.0)*2.*PI-PI/2.)*120+yc);
  if(dy - yc >= 0)
  	dy+=charsize;
  else
  	dy-=charsize/2;
  if(dx -xc >=0)
  	dx+=charsize/2;
  else
setfillstyle(1,4);
 dx-=charsize;
 moveto(midx,midy);
 lineto(dx,dy);
 setcolor(BLUE);
}
void hour_hand(int midx, int midy,int d)
{
int dx = (int) (cos((d/60.0)*2.*PI-PI/2.)*100+xc);
  int dy = (int) (sin((d/60.0)*2.*PI-PI/2.)*100+yc);
  if(dy - yc >= 0)
  	dy+=charsize;
  else
  	dy-=charsize/2;
  if(dx -xc >=0)
  	dx+=charsize/2;
  else
setfillstyle(1,4);
 dx-=charsize;
 moveto(midx,midy);
 lineto(dx,dy);
 setcolor(GREEN);
}
```

