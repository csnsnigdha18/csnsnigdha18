Tic-Tac-Toe Game Code...............
#include <stdio.h>
#include <conio.h>

int s[3][3] = {{0,0,0},{0,0,0},{0,0,0}};
char d[3][3] = {{' ',' ',' '}, {' ',' ',' '}, {' ',' ',' '}};
char xo,y;              //Computer move is denoted by 'y'.
int winner();
void game();
int computer_move();
int attack();
int defence();

int main()
{
    int player = 1,b,r,c;   //'b' denotes getting the value from winner method.
    printf("Select the choice 'X' or 'O' :\n");
        scanf("%c",&xo);
       b=winner();
       
    while(b==2)
    {
        game();
        player = (player % 2) ? 1 : 2;
        if(xo == 'x' || xo == 'X')              //players choice 
        y='O';                                  //computers choice
        else if(xo == 'o' || xo == 'O')
        y='X';
        if(xo == 'x' || xo == 'X')
        {
            if(player==1)
            {
            printf("Enter the position :");
        scanf("%d %d",&r,&c);
        if (s[r][c] == 0)
            {
                if(xo == 'x' || xo == 'X')        //or if(y=='O')
                {
                    s[r][c]=1;
                    d[r][c]='X';
                }
                
                else if(xo == 'o' || xo == 'O')   //or if(y=='X')
                {
                    s[r][c]=-1;
                    d[r][c]='O';
                }
            }
            
        else
        {
            printf("Invalid move.");

            player--;
            getch();
        }

        b = winner();

        player++;
        }
        else if(player==2)
        {
            computer_move();

        b = winner();

        player++;
        }
        }
        else if(xo == 'o' || xo =='O')      //or if(y=='X')
        {
            if(player==1)
            {
                computer_move();

        b = winner();

        player++;
            }
            else if(player==2)
            {
            printf("Enter the position :");
        scanf("%d %d",&r,&c);
        if (s[r][c] == 0)
            {
                if(xo == 'x' || xo == 'X')   //or if(y=='O')
                {
                    s[r][c]=1;
                    d[r][c]='X';
                }
                
                else if(xo == 'o' || xo == 'O')   //or if(y=='X')
                {
                    s[r][c]=-1;
                    d[r][c]='O';
                }
            }
            
        else
        {
            printf("Invalid move.");

            player--;
            getch();
        }

        b = winner();

        player++;
        }
        }
        
    }
    
    game();
    if(b==1)          
    {
    if (xo == 'x' || xo == 'X')       //or if(y=='O')
        printf("==>\aYou won ");
    else if(xo == 'o' || xo == 'O')
        printf("==>\aComputer won");
    }
    else if(b==-1)      
    {
    if (xo == 'o' || xo =='O')        //or if(y=='X')
        printf("==>\aYou won ");
    else if(xo == 'x' || xo =='X')
        printf("==>\aComputer won");
    }
    else if(b==0)
        printf("==>\aGame draw");

    getch();

    return 0;
}

//Computer method begins here........which includes attack and defence methods.
int computer_move()
{
    if(y == 'O')
    {
        int ld=0,rd=0,c=0;
        for(int i=0;i<3;i++)
        {
        //'ld' and 'rd' are sum of the left diagonal and right diagonal elements respectively.
            int sr=0,sc=0;          //'sr' and 'sc' are sum of row and column respectively.
            for(int j=0;j<3;j++)
            {
                if(i==j)            //Condition for left diagonal.
                ld = ld + s[i][j];
                if(i+j==2)          //Condition for right diagonal.
                rd = rd + s[i][j];
                sr = sr + s[i][j];
                sc = sc + s[j][i];
            }
                if(sr==2 || sc==2 || ld==2 || rd==2)
                c++;
        }
        if(c>0)
        {
            defence();
        }
        else
        {
            attack();
        }
    }
    else if(y == 'X')
    {
        int ld=0,rd=0,c=0;
        for(int i=0;i<3;i++)
        {
        //'ld' and 'rd' are sum of the left diagonal and right diagonal elements respectively.
            int sr=0,sc=0;      
            for(int j=0;j<3;j++)
            {
                if(i==j)
                ld = ld + s[i][j];
                if(i+j==2)
                rd = rd + s[i][j];
                sr = sr + s[i][j];
                sc = sc + s[j][i];
            }
                if(sr==-2 || sc==-2 || ld==-2 || rd==-2)
                c++;
        }
        if(c>0)
        {
            defence();
        }
        else
        {
            attack();
        }
        game();
    }
    return 0;
}

//Attack method begins here...................
int attack()
{
    if(y=='O')      //or if(xo=='x' || xo=='X')
    {
        int rm[3]={0,0,0},cm[3]={0,0,0};
        int ld=0,rd=0,c=0,rmin=0,cmin=0,ri=0,ci=0,min=0,mini=0;
        /* 'rm' is row max amd 'cm' is column max.
           'rmin' is row min and 'cmin' is column min.
           'ri' is row index and 'ci' is column index.
           'min' is the minimum value.
           'mini' is the minimum index. */
        for(int i=0;i<3;i++)
        {
            int sr=0,sc=0;      
            for(int j=0;j<3;j++)
            {
                if(i==j)
                ld = ld + s[i][j];
                if(i+j==2)
                rd = rd + s[i][j];
                sr = sr + s[i][j];
                sc = sc + s[j][i];
                c++;
            }
            rm[c]=sr;
            cm[c]=sc;
        }
        rmin=rm[0];
        for(int i=0;i<3;i++)
        {
            if(rm[i]<rmin)
            {
                ri=i;
            }
        }
        cmin=cm[0];
        for(int i=0;i<3;i++)
        {
            if(cm[i]<cmin)
            {
                ci=i;
            }
        }
        int tot[4]={rm[ri],cm[ci],ld,rd};
        min=tot[0];
        for(int i=0;i<4;i++)
        {
            if(tot[i]<min)
            {
                mini=i;
            }
        }
        if(mini==0)
        {
            for(int j=0;j<3;j++)
            if(d[ri][j]==' ')
            {
                d[ri][j]='O';
                s[ri][j]=-1;
            }
        }
        else if(mini==1)
        {
            for(int i=0;i<3;i++)
            if(d[i][ci]==' ')
            {
                d[i][ci]='O';
                s[i][ci]=-1;
            }
        }
        else if(mini==2)
        {
            for(int i=0;i<3;i++)
            {
                for(int j=0;j<3;j++)
                if(i==j && d[i][j]==' ')
                {
                    d[i][j]='O';
                    s[i][j]=-1;
                }
                
            }
        }
        else
        {
            for(int i=0;i<3;i++)
            {
                for(int j=0;j<3;j++)
                if(i+j==2 && d[i][j]==' ')
                {
                    d[i][j]='O';
                    s[i][j]=-1;
                }
            }
        }
    }
    else if(y=='X')
    {
        int rm[3]={0,0,0},cm[3]={0,0,0};
        int ld=0,rd=0,c=0,rmax=0,cmax=0,ri=0,ci=0,max=0,maxi=0;
        for(int i=0;i<3;i++)
        {
            int sr=0,sc=0;      
            for(int j=0;j<3;j++)
            {
                if(i==j)
                ld = ld + s[i][j];
                if(i+j==2)
                rd = rd + s[i][j];
                sr = sr + s[i][j];
                sc = sc + s[j][i];
                c++;
            }
            rm[c]=sr;
            cm[c]=sc;
        }
        rmax=rm[0];
        for(int i=0;i<3;i++)
        {
            if(rm[i]>rmax)
            {
                ri=i;
            }
        }
        cmax=cm[0];
        for(int i=0;i<3;i++)
        {
            if(cm[i]>cmax)
            {
                ci=i;
            }
        }
        int tot[4]={rm[ri],cm[ci],ld,rd};
        max=tot[0];
        for(int i=0;i<4;i++)
        {
            if(tot[i]>max)
            {
                maxi=i;
            }
        }
        if(maxi==0)
        {
            for(int j=0;j<3;j++)
            if(d[ri][j]==' ')
            {
                d[ri][j]='X';
                s[ri][j]=1;
            }
        }
        else if(maxi==1)
        {
            for(int i=0;i<3;i++)
            if(d[i][ci]==' ')
            {
                d[i][ci]='X';
                s[i][ci]=1;
            }
        }
        else if(maxi==2)
        {
            for(int i=0;i<3;i++)
            {
                for(int j=0;j<3;j++)
                if(i==j && d[i][j]==' ')
                {
                    d[i][j]='X';
                    s[i][j]=1;
                }
            }
        }
        else
        {
            for(int i=0;i<3;i++)
            {
                for(int j=0;j<3;j++)
                if(i+j==2 && d[i][j]==' ')
                {
                    d[i][j]='X';
                    s[i][j]=1;
                }
            }
        }
    }
    return 0;
}

//Defence method starts here..................
int defence()
{
    if(y=='X')
    {
        int ld=0,rd=0,rs[3]={0,0,0},cs[3]={0,0,0};
        for(int i=0;i<3;i++)
        {
            int sr=0,sc=0;
            for(int j=0;j<3;j++)
            {
                if(i==j)
                ld = ld + s[i][j];
                if(i+j==2)
                rd = rd + s[i][j];
                sr = sr + s[i][j];
                sc = sc + s[i][j];
            }
            rs[i]=sr;
            cs[i]=sc;
        }
        for(int i=0;i<3;i++)
        {
            if(rs[i]==-2)
            {
               for(int j=0;j<3;j++)
               {
                   if(d[i][j]==' ')
                   {
                       d[i][j]='X';
                       s[i][j]=1;
                   }
               }
            }
            else if(cs[i]==-2)
            {
               for(int j=0;j<3;j++)
               {
                   if(d[j][i]==' ')
                   {
                       d[j][i]='X';
                       s[j][i]=1;
                   }
               }
            }
            else if(ld==-2)
            {
               for(int j=0;j<3;j++)
               {
                   if(d[i][j]==' ' && i==j)
                   {
                       d[i][j]='X';
                       s[i][j]=1;
                   }
               }
            }
            else if(rd==-2)
            {
               for(int j=0;j<3;j++)
               {
                   if(d[i][j]==' ' && i+j==2)
                   {
                       d[i][j]='X';
                       s[i][j]=1;
                   }
               }
            }
        }
    }
    else if(y=='O')
    {
        int ld=0,rd=0,rs[3]={0,0,0},cs[3]={0,0,0};
        for(int i=0;i<3;i++)
        {
            int sr=0,sc=0;
            for(int j=0;j<3;j++)
            {
                if(i==j)
                ld = ld + s[i][j];
                if(i+j==2)
                rd = rd + s[i][j];
                sr = sr + s[i][j];
                sc = sc + s[i][j];
            }
            rs[i]=sr;
            cs[i]=sc;
        }
        for(int i=0;i<3;i++)
        {
            if(rs[i]==2)
            {
               for(int j=0;j<3;j++)
               {
                   if(d[i][j]==' ')
                   {
                       d[i][j]='O';
                       s[i][j]=1;
                   }
               }
            }
            else if(cs[i]==2)
            {
               for(int j=0;j<3;j++)
               {
                   if(d[j][i]==' ')
                   {
                       d[j][i]='O';
                       s[j][i]=1;
                   }
               }
            }
            else if(ld==2)
            {
               for(int j=0;j<3;j++)
               {
                   if(d[i][j]==' ' && i==j)
                   {
                       d[i][j]='O';
                       s[i][j]=1;
                   }
               }
            }
            else if(rd==2)
            {
               for(int j=0;j<3;j++)
               {
                   if(d[i][j]==' ' && i+j==2)
                   {
                       d[i][j]='O';
                       s[i][j]=1;
                   }
               }
            }
        }
    }
    return 0;
}
/*********************************************
FUNCTION TO RETURN GAME STATUS
1 FOR 'X' player
-1 FOR 'O' player
0 if GAME IS OVER AND NO RESULT, which is a Draw.
 **********************************************/

int winner()
{
    int count=0,c=0,ld=0,rd=0;
    for(int i=0;i<3;i++)
    {
        int sr=0,sc=0;
        for(int j=0;j<3;j++)
        {
            c+=s[i][j];
            sr+= s[i][j];
            sc+= s[j][i];
            if(i==j)
            ld+=s[i][j];
            else if(i+j==2)
            rd+=s[i][j];
            count++;
        }
        if(sr==3||sc==3||ld==3||rd==3)
        {
           return 1;break;
        }
        else if(sr==-3||sc==-3||ld==-3||rd==-3)
        {
            return -1;break;
        }
    }
    if(count==9)
        return 2;
    else if(c==1)
        return 0;
}


/*******************************************************************
FUNCTION TO DRAW BOARD OF TIC TAC TOE WITH SYMBOLS
 ********************************************************************/


void game()
 {
    printf("\n\n\tTic Tac Toe\n\n");
    if(xo == 'x' || xo == 'X')
    printf("Player 1 (X)  - Computer (O) \n\n\n");
    else if(xo == 'o' || xo == 'O')
    printf("Player 1 (O)  - Computer (X) \n\n\n");

    printf("     |     |     \n");
    printf("  %c  |  %c  |  %c \n", d[0][0], d[0][1], d[0][2]);

    printf("_____|_____|_____\n");
    printf("     |     |     \n");

    printf("  %c  |  %c  |  %c \n", d[1][0], d[1][1], d[1][2]);

    printf("_____|_____|_____\n");
    printf("     |     |     \n");

    printf("  %c  |  %c  |  %c \n", d[2][0], d[2][1], d[2][2]);

    printf("     |     |     \n\n");
    
}

/*******************************************************************
END OF PROJECT
 ********************************************************************/
 
