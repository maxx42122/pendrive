#include<iostream>
#include<graphics.h>
#include<math.h>
using namespace std;

class figure
{
	float length,delx,dely;
	int d,h,xc,yc;
	public:
	void drawline(float x1,float y1,float x2,float y2) //ddaline
	{
		float x,y;
		if(abs(x2-x1)>=abs(y2-y1))
		{
			length=abs(x2-x1);
		}
		else
		{
			length=abs(y2-y1);
		}
		delx=(x2-x1)/length;  
		dely=(y2-y1)/length;

		x=x1+0.5; 
		y=y1+0.5;

		putpixel(floor(x),floor(y),WHITE);

		int i=1;
		while(i<=length) 
		{
			x=x+delx;
			y=y+dely;
			i=i+1;
			putpixel(floor(x),floor(y),WHITE);
	}  

} // end ddaline
void drawcircle(int r,int xc,int yc)//Bresenham circle
{
		int x,y;    
		d=3-2*r;
		x=0;
		y=r;
		do
		{
			putpixel(x+xc,y+yc,WHITE); //symmentry approach
			putpixel(y+xc,x+yc,WHITE);
			putpixel(y+xc,-x+yc,WHITE);
			putpixel(x+xc,-y+yc,WHITE);
			putpixel(-x+xc,-y+yc,WHITE);
			putpixel(-y+xc,-x+yc,WHITE);
			putpixel(-y+xc,x+yc,WHITE);
			putpixel(-x+xc,y+yc,WHITE);
		if(d<0)
		{
			d=d+4*x+6;
			x=x+1;
		}
		else 
		{
			d=d+4*(x-y)+10;
			y=y-1;
			x=x+1;
		}
		}while(x<=y);
		}// end of circle algorithm

void fig(float x11,float y11,float length){
	h=((sqrt(3))*length)/2;
	drawline(x11,y11,x11+length,y11);
	drawline(x11+length,y11,x11+(length)/2,y11-h);
	drawline(x11,y11,x11+(length)/2,y11-h);
	drawcircle(h/3,x11+(length)/2,y11-(h/3));
	drawcircle(2*h/3,x11+(length)/2,y11-(h/3));
	}
};

int main()
{
	figure f1;
	float x1,y1,length;
	cout<<"enter the coordinates=";
	cin>>x1>>y1;
	cout<<"enter the length=";
	cin>>length;
	int gd=DETECT,gm;
	initgraph(&gd,&gm,NULL);
	f1.fig(x1,y1,length);
	getch();
	closegraph();
	return 0;
}


//////////
DDA algorithm is a line drawing algorithm used in computer graphics to generate a line segment between two specified endpoints. It is a simple and efficient algorithm that works by using the incremental difference between the x-coordinates and y-coordinates of the two endpoints to plot the line. The algorithm is based on the principle that the slope of the line is equal to the ratio of the change in y to the change in x. The algorithm calculates the intermediate points along the line by adding a small fraction of the slope to the previous point. The algorithm can handle any line with any slope, but it may not produce accurate results for steep lines or vertical lines. The algorithm also requires floating-point arithmetic, which can be slow on some systems. The algorithm can be summarized as follows:

- Input the two endpoints of the line segment, (x1,y1) and (x2,y2).
- Calculate the difference between the x-coordinates and y-coordinates of the endpoints as dx and dy respectively.
- Calculate the slope of the line as m = dy/dx.
- Set the initial point of the line as (x1,y1).
- Loop through the x-coordinates of the line, incrementing by one each time, and calculate the corresponding y-coordinate using the equation y = y1 + m (x – x1).
- Plot the pixel at the calculated (x,y) coordinate.
- Repeat steps 5 and 6 until the endpoint (x2,y2) is reached.

//////

The Bresenham's circle drawing algorithm is a
circle drawing algorithm which calculates all
the nearest points nearest to the circle
boundary.
 It is an incremental method (i.e. we increment
one of the coordinates of the point and calculate
the other coordinate according to it.
 It only uses integer arithmetic which makes
it's working faster as well as less complex.
 The strategy that is followed in this algorithm is
to select the pixel which has the least distance
with the true circle boundary and with then keep
calculating the successive points on the circle
///////////
The figure class is defined, which contains methods for drawing a line (drawline), drawing a circle using Bresenham's circle algorithm (drawcircle), and drawing a specific geometric figure (fig).

The drawline method uses the DDA (Digital Differential Analyzer) algorithm to draw a line between two points.

The drawcircle method implements Bresenham's circle-drawing algorithm to draw a circle.

The fig method draws a specific geometric figure. It consists of three lines and two circles. The figure is drawn based on the input coordinates (x1 and y1) and the length of the lines.

In the main function, an instance of the figure class (f1) is created, and the user is prompted to enter the coordinates and length of the figure.

The graphics window is initialized using the initgraph function from the graphics.h library.

The fig method is called to draw the geometric figure.

The program waits for user input with getch() and then closes the graphics window with closegraph().

//////////////

### DDA Line Drawing Algorithm:

1. *Input:*
   - (x1, y1) and (x2, y2) are the coordinates of the two endpoints of the line.

2. *Calculate differences:*
   - Calculate the differences dx = x2 - x1 and dy = y2 - y1.

3. *Determine steps and increments:*
   - Determine the number of steps, N, based on the larger of |dx| and |dy|.
   - Calculate increments for x and y as incX = dx/N and incY = dy/N.

4. *Initialize variables:*
   - Set x = x1 and y = y1.

5. *Draw points:*
   - For i from 1 to N, draw the point (round(x), round(y)).
   - Update x by adding incX and y by adding incY.

### Example:

Let's consider two points: (2, 3) and (8, 12).

1. Calculate differences: dx = 8 - 2 = 6, dy = 12 - 3 = 9.

2. Determine steps and increments: N = max(|6|, |9|) = 9.
   - incX = 6/9 = 2/3, incY = 9/9 = 1.

3. Initialize variables: x = 2, y = 3.
a
4. Draw points:
   - Point 1: (round(2), round(3)) = (2, 3)
   - Point 2: (round(2 + 2/3), round(3 + 1)) = (3, 4)
   - ...
   - Point 9: (round(8), round(12)) = (8, 12)
//////////////////////////

### Bresenham's Circle Algorithm:

1. *Input:* Center coordinates (x_center, y_center), radius (r).
2. *Initialization:*
   - Set x = 0
   - Set y = r
   - Set decision parameter P = 3 - 2*r

3. *Draw Initial Pixel:*
   - Plot the pixel at coordinates (x_center + x, y_center - y)

4. *Iteration:*
   - While x <= y:
     - If P < 0, increment x and update P as P = P + 4*x + 6.
     - If P ≥ 0, increment x and decrement y, update P as P = P + 4*(x - y) + 10.
     - Plot the symmetric points in the other octants as well.

5. *Repeat until x > y*



