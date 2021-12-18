# translation-in-c-using-matrix-
  
#include<stdio.h>
#include<conio.h>
#include<graphics.h>
void translatedCoordinate(int T[][3], int P[][1]);
void translate(int x[], int y[], int tx, int ty);

int main()
{
     int x[100]={0};
	 int y[100]={0};
	 printf("enter the coordinated of the points of triangle to be translated");
     for(int i=0;i<3;i++){
        scanf("%d %d",&x[i],&y[i]);
       }
     
    int tx,ty;
    printf("enter the value of tx and ty:");
    scanf("%d%d",&tx,&ty);
    
    int gd,gm;
    detectgraph(&gd,&gm);
    initgraph(&gd,&gm,"C:\\TURBOC3\\BGI\\");
    translate(x,y,tx,ty);
    getch();
 
 }

  void translatedCoordinate(int T[][3], int P[][1])
{
  int temp[3][1] = { 0 };


     for (int i =0; i < 3; i++)
	 for (int j =0; j < 1; j++)    
     for (int k =0; k < 3; k++)	     
     temp[i][j] += (T[i][k] * P[k][j]);
	 
	 

    P[0][0] = temp[0][0];
    P[1][0] = temp[1][0];
    P[2][0] = 1;

}
      // Scaling the Polygon
  void translate(int x[], int y[], int tx, int ty)
 {    setcolor(RED);
      // Triangle before translation
     line ( x[0], y[0], x[1], y[1]);
     line ( x[1], y[1], x[2], y[2]);
     line ( x[2], y[2], x[0], y[0]);
      // Initializing the translation Matrix.
     int T[3][3] = { 1, 0, tx ,0 ,1 ,ty ,0 , 0 ,1 };
     int P[3][1];

     // translating the triangle
     for (int i =0; i < 3; i++)
   {
      P[0][0] = x[i];
      P[1][0] = y[i];
       translatedCoordinate(T, P);
      x[i] = P[0][0];
      y[i] = P[1][0];
   }
   setcolor(GREEN);
     // Triangle after translating
    line ( x[0], y[0], x[1], y[1]);
    line ( x[1], y[1], x[2], y[2]);
    line ( x[2], y[2], x[0], y[0]);
}
