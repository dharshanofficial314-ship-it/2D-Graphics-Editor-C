#include <stdio.h>
#include <stdlib.h>
#include <math.h>

#define ROWS 25
#define COLS 60

char canvas[ROWS][COLS];

void initializeCanvas()
{
    int i,j;

    for(i=0;i<ROWS;i++)
    {
        for(j=0;j<COLS;j++)
        {
            canvas[i][j]='_';
        }
    }
}

void displayCanvas()
{
    int i,j;

    for(i=0;i<ROWS;i++)
    {
        for(j=0;j<COLS;j++)
        {
            printf("%c",canvas[i][j]);
        }
        printf("\n");
    }
}

void drawRectangle(int row,int col,int width,int height)
{
    int i,j;

    for(i=row;i<row+height;i++)
    {
        for(j=col;j<col+width;j++)
        {
            if(i==row || i==row+height-1 ||
               j==col || j==col+width-1)
            {
                if(i>=0 && i<ROWS && j>=0 && j<COLS)
                    canvas[i][j]='*';
            }
        }
    }
}

void drawLine(int row,int startCol,int endCol)
{
    int i;

    for(i=startCol;i<=endCol;i++)
    {
        if(row>=0 && row<ROWS && i>=0 && i<COLS)
            canvas[row][i]='*';
    }
}

void drawTriangle(int row,int col,int height)
{
    int i,j;

    for(i=0;i<height;i++)
    {
        for(j=-i;j<=i;j++)
        {
            if(i==height-1 || j==-i || j==i)
            {
                if(row+i<ROWS && col+j>=0 && col+j<COLS)
                    canvas[row+i][col+j]='*';
            }
        }
    }
}

void drawCircle(int centerRow,int centerCol,int radius)
{
    int x,y;

    for(x=0;x<ROWS;x++)
    {
        for(y=0;y<COLS;y++)
        {
            int dx=x-centerRow;
            int dy=y-centerCol;

            double dist=sqrt(dx*dx+dy*dy);

            if(dist>=radius-0.5 && dist<=radius+0.5)
            {
                canvas[x][y]='*';
            }
        }
    }
}

void deleteArea(int row,int col,int width,int height)
{
    int i,j;

    for(i=row;i<row+height;i++)
    {
        for(j=col;j<col+width;j++)
        {
            if(i>=0 && i<ROWS && j>=0 && j<COLS)
                canvas[i][j]='_';
        }
    }
}

int main()
{
    int choice;

    initializeCanvas();

    while(1)
    {
        printf("\n===== 2D GRAPHICS EDITOR =====\n");
        printf("1. Draw Rectangle\n");
        printf("2. Draw Line\n");
        printf("3. Draw Triangle\n");
        printf("4. Draw Circle\n");
        printf("5. Delete Area\n");
        printf("6. Clear Canvas\n");
        printf("7. Display Canvas\n");
        printf("8. Exit\n");

        printf("Enter Choice: ");
        scanf("%d",&choice);

        switch(choice)
        {
            case 1:
            {
                int r,c,w,h;

                printf("Row Col Width Height: ");
                scanf("%d%d%d%d",&r,&c,&w,&h);

                drawRectangle(r,c,w,h);
                break;
            }

            case 2:
            {
                int row,start,end;

                printf("Row StartCol EndCol: ");
                scanf("%d%d%d",&row,&start,&end);

                drawLine(row,start,end);
                break;
            }

            case 3:
            {
                int row,col,height;

                printf("Row Col Height: ");
                scanf("%d%d%d",&row,&col,&height);

                drawTriangle(row,col,height);
                break;
            }

            case 4:
            {
                int row,col,radius;

                printf("CenterRow CenterCol Radius: ");
                scanf("%d%d%d",&row,&col,&radius);

                drawCircle(row,col,radius);
                break;
            }

            case 5:
            {
                int r,c,w,h;

                printf("Row Col Width Height: ");
                scanf("%d%d%d%d",&r,&c,&w,&h);

                deleteArea(r,c,w,h);
                break;
            }

            case 6:
            {
                initializeCanvas();
                break;
            }

            case 7:
            {
                displayCanvas();
                break;
            }

            case 8:
            {
                printf("Exiting...\n");
                return 0;
            }

            default:
            {
                printf("Invalid Choice\n");
            }
        }
    }

    return 0;
}
