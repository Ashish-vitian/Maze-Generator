# Maze-Generator
An graph based Maze Generator and solver coded in java

import java.util.*;
import java.util.Random;
import java.util.Scanner;
public class Mazegenerator 
{
	void maze_generator(int index,int[][] maze,int[] backtrack_x,int[] backtrack_y,int x,int y,int n,int visited,int MAX)
	{
	
  
	{
		int z=n*n;
		if(visited<z)	
		{
			int step[]=new int[4];			
			int neighbour_valid=-1;
			int x_next = 0;
			int y_next=0;
			int[] neighbour_x=new int[4];
			int[] neighbour_y=new int[4];
			closemaze obj=new closemaze();
			boolean m=obj.is_closed(maze,x-2,y,MAX);			
			if(x-2>0 && m==true)                      //upside
			{
				neighbour_valid++;
				neighbour_x[neighbour_valid]=x-2;
				neighbour_y[neighbour_valid]=y;
				step[neighbour_valid]=1;
				
			}
			boolean h=obj.is_closed(maze,x,y-2,MAX);       /*leftside*/
			if(y-2>0 && h==true)            
			{
				neighbour_valid++;
				neighbour_x[neighbour_valid]=x;
				neighbour_y[neighbour_valid]=y-2;
				step[neighbour_valid]=2;
				
			}
			
			boolean l=obj.is_closed(maze,x,y+2,MAX);
			if(y+2<n*2+1 && l==true)    //rightside
			{
				neighbour_valid++;
				neighbour_x[neighbour_valid]=x;
				neighbour_y[neighbour_valid]=y+2;
				step[neighbour_valid]=3;			
			}
			
			boolean u=obj.is_closed(maze,x+2,y,MAX);
			if(x+2<n*2+1 && u==true)    //downside
			{
				neighbour_valid++;
				neighbour_x[neighbour_valid]=x+2;
				neighbour_y[neighbour_valid]=y;
				step[neighbour_valid]=4;
			}
			if(neighbour_valid==-1)
			{
				
				if(index>0)
				{
				x_next=backtrack_x[index];
				y_next=backtrack_y[index];
				}
				index--;
			}
			if(neighbour_valid!=-1)
			{
				Random randomGenerator=new Random();
				int randomization=neighbour_valid+1;
				int randomInt=randomGenerator.nextInt(randomization);	
				x_next=neighbour_x[randomInt];
				y_next=neighbour_y[randomInt];
				index=index+1;
				backtrack_x[index]=x_next;
				backtrack_y[index]=y_next;
				int rstep=step[randomInt];
				/*if(rstep==1);
				{
					maze[x_next+1][y_next]=0;
					System.out.println("rstep1");
				}
				if(rstep==2);
				{
				    maze[x_next][y_next+1]=0;
				    System.out.println("rstep2");
				}
				if(rstep==3)
				{
				    maze[x_next][y_next-1]=0;
				    System.out.println("rstep3");
				}
				if(rstep==4)
				{
					maze[x_next-1][y_next]=0;
					System.out.println("rstep4");
				}*/
				switch(rstep){
				case 1:
					maze[x_next+1][y_next]=0;
					break;
				case 2:
					maze[x_next][y_next+1]=0;
				    break;
				case 3:
					maze[x_next][y_next-1]=0;
				    break;
				case 4:
					maze[x_next-1][y_next]=0;
					break;
					
				}
				visited++;
			}
			maze_generator(index, maze, backtrack_x, backtrack_y, x_next, y_next, n, visited,MAX);
	                                                                                                   
		}
		
	}
}
}
class printmaze 
{
	printmaze(int[][] maze, int maze_size)
	{
	     for(int a = 0; a < maze_size * 2 + 1; a++)
	     {
	         for(int b = 0; b < maze_size * 2 + 1; b++)
	         {
	             if(maze[a][b] == 1)
	                 System.out.print(maze[a][b]);
	            else
	                 System.out.print(0);
	         }
	         System.out.println();
	     }
	}
}
class closemaze 
{
	boolean a=false;

	boolean is_closed(int[][] maze,int m,int n,int MAX)
	   {
		    int WALL=1;
		    if(m>0 && n>0 && m<MAX && n<MAX)
		    {
			 if(maze[m-1][n]==WALL && maze[m][n-1]==WALL && maze[m][n+1]==WALL && maze[m+1][n]==WALL)
			       {
				               return true;
			       }
		   }
		    
          return false; 
	   }
}
	
class init_maze {
	void hello_maze(int[][] maze,int MAX)
	{
		 /*this.MAX=MAX;
		 this.maze=new int[this.MAX][this.MAX]; */
	     for(int a = 0; a < MAX; a++)
	      {
	         for(int b = 0; b < MAX; b++)
	           {
	             if(a % 2 == 0 || b % 2 == 0)
	             {
	                maze[a][b] = 1;
	             }
	                else
	                {
	                maze[a][b] = 0;
	                }
	         }
	     }
	}

}




class mazee
{
	private int N;
int solveMazeUtil(int maze[][], int x, int y, int sol[][])
{
	// if (x,y is goal) return true
	if(x == N-1 && y == N-1)/*here we checking whether the exist path is their or not*/
	{
		sol[x][y] = 1;
		return 1;
	}

	// Check if maze[x][y] is valid
	if(isSafe(maze, x, y) == 1)
	{
		// mark x,y as part of solution path
		sol[x][y] = 1;

		/* Move forward in x direction */
		if (solveMazeUtil(maze, x+1, y, sol) ==1)
			return 1;

		/* If moving in x direction doesn't give solution then
		Move down in y direction */
		if (solveMazeUtil(maze, x, y+1, sol) ==1)
			return 1;

		/* If none of the above movements work then BACKTRACK: 
			unmark x,y as part of solution path */
		sol[x][y] = 0;
		return 0;
	} 

	return 0;
}
public int solveMaze(int maze[][],int n)
{
try{
	        if (maze == null) {
	            throw new NullPointerException("The input maze cannot be null");
	        }
}
catch(NullPointerException e)/*throwing exception if null value is their*/
{
	System.out.println(""+e);
}
	    
	this.N=n;
	int sol[][]=new int[N][N];
	for(int x=0;x<N;x++)
	{
		for(int y=0;y<N;y++)/*here we are creating a second maze with default value zero means wall*/
		{
			sol[x][y]=0;
			
		}
	}
/*nt sol[][]= { {0, 0, 0, 0},
		{0, 0, 0, 0},
		{0, 0, 0, 0},
		{0, 0, 0, 0}
	};*/

	if(solveMazeUtil(maze, 0, 0, sol) == 0)
	{
		System.out.println("Solution doesn't exist");
		return 0;
	}

	printSolution(sol);
	return 0;
}
void printSolution(int sol[][])
{
	for (int i = 0; i < N; i++)
	{
		for (int j = 0; j < N; j++)
		{
			if(sol[i][j]==1)
			{
			System.out.print("-");
			}
			else
			{
				System.out.print("#");
			}
		}
		System.out.print("\n");
	}
}
public void changemaze(int maze[][],int n)
{
	
}
/* A utility function to check if x,y is valid index for N*N maze */
int isSafe(int maze[][], int x, int y)
{
	// if (x,y outside maze) return false
	if(x >= 0 && x < N && y >= 0 && y < N && maze[x][y] == 1)/*we are checking whether the given path is valid or not*/
		return 1;
	else
		
	return 0;
}
}
class Maze {
	public static void main(String args[])
	{
	Scanner sc=new Scanner(System.in);
	int g;
	
		final int Cell=900;
		int size;
		int index=0;
		
		System.out.println("Maze Creator");
		System.out.println("Input(0~30)");
		@SuppressWarnings("resource")
		Scanner s=new Scanner(System.in);
		System.out.println("Enter Size n to generate the maze of(2*n+1)");
		size=s.nextInt();
        int MAX=2*size+1;
		int[][] maze;
		maze=new int[MAX][MAX];
	    int backtrack_x[];
	    backtrack_x=new int[Cell];
		int backtrack_y[];
		backtrack_y=new int[Cell];
		init_maze obj1=new init_maze();
		obj1.hello_maze(maze,MAX);
		int maze1[][];
		maze1=new int[MAX][MAX];
		backtrack_x[index]=1;
		backtrack_y[index]=1;
		int maze4[][];
		maze4=new int[MAX-2][MAX-2];
		g=MAX-2;
		int maze3[][];
		maze3=new int[g][g];
		Mazegenerator obj2=new Mazegenerator();
	    obj2.maze_generator(index,maze,backtrack_x,backtrack_y,1,1,size,1,MAX); 
		printmaze obj=new printmaze(maze,size);
		System.out.println("Maze without wall");
		for(int i=1;i<MAX-1;i++)
		{
			for(int j=1;j<MAX-1;j++)
			{
				maze1[i][j]=maze[i][j];
				System.out.print(maze1[i][j]);
			}
			System.out.println();
		}
		for(int i=0;i<MAX-2;i++)
		{
			for(int j=0;j<MAX-2;j++)
			{
				maze3[i][j]=maze1[i+1][j+1];
				
			}
	
		}
		for(int i=0;i<MAX-2;i++)
		{
			for(int j=0;j<MAX-2;j++)
			{
				System.out.print(maze3[i][j]);
			}
			System.out.println();
		}
		for(int i=0;i<MAX-2;i++)
		{
			for(int j=0;j<MAX-2;j++)
			{
				maze4[i][j]=maze3[i][j];
				if(maze4[i][j]==0)
				{
					maze4[i][j]=1;
					
				}
				else
				{
					maze4[i][j]=0;
				}
				
			}
	
		}
		System.out.println("coverted maze");
		for(int i=0;i<MAX-2;i++)
		{
			for(int j=0;j<MAX-2;j++)
			{
				System.out.print(maze4[i][j]);
			}
			System.out.println();
		}
		System.out.println("solved maze");
		
	/*	for(int i=1;i<MAX-1;i++)
		{
			for(int j=1;j<MAX-1;j++)
			{
				if(maze3[i][j]==0)
					
				{
					maze3[i][j]=1;
				}
				else
					
				{
					maze3[i][j]=0;
				}
			}
		}
		System.out.println("after coverting 1 as path and 0 as wall");
		for(int i=1;i<MAX-1;i++)
		{
			for(int j=1;j<MAX-1;j++)
			{
				System.out.print(maze3[i][j]);
			}
			System.out.println();
		}
	System.out.println("maze with soln");
	{
		
		/*System.out.println("enter the size of maze yu want to enter");/*entering the maze size*/
		/*int n=sc.nextInt();
		int[][] maze=new int[n][n];
		for(int x=0;x<n;x++)/*we are taking input of the maze from the user */
		/*{
			for(int y=0;y<n;y++)
			{
				System.out.println("enter the maze element");
				maze[x][y]=sc.nextInt();/*declaration of the maze*/
	
	mazee m=new mazee();/*here we are creating a reference variable and assigning it the address value*/
	/*int maze[][] = {
		      { 1, 0, 0, 0 },
		      { 1, 1, 0, 1 },
		      { 0, 1, 1, 1 },
		      { 0, 1, 0, 1 } };*/
	m.solveMaze(maze4,g);/*passing the value to the function of another class by using it object*/
	
   
	
	}
}

