# TicTacToe Game


#Title : This programe is about Implement a Tic-Tac -Toe game in which user is going to play with computer by applying its Intelligent



import java.util.*;
public class MainClass 
{
	int mat[][]=new int[3][3]; //for 3x3 Card for Tic-Tac -Toe 
	Scanner sc=new Scanner(System.in);
	int userSymbol; //code is done by putting userSymbol as '1' and machine will put '2'
	int i,j;
	
	
	void getData() //get the initial data
	{
		System.out.println("Enter Which is your symbol either 1 or 2");
		userSymbol=sc.nextInt();
	
	}
	
	int isWin()  //checks is their anyone i.e player or Computer is winning or not
	{
		int res=0;
		for(int i=0;i<3;i++)
		{
			if(mat[i][0]!=0 && mat[i][1]!=0 && mat[i][2]!=0 && mat[i][0]==mat[i][1] && mat[i][1]==mat[i][2] ) //for row
			{
				res=1;
				System.out.println("Winner:"+mat[i][0]);
				break;
			}
			else if(mat[0][i]!=0 && mat[1][i]!=0 && mat[2][i]!=0  && mat[0][i]==mat[1][i] && mat[1][i]==mat[2][i]) //for column
			{
				res=1;
				System.out.println("Winner:"+mat[1][i]);
				break;
			}
		}
		if(res==0)
		{
			if( mat[0][0]!=0 && mat[1][1]!=0 && mat[2][2]!=0 && mat[0][0]==mat[1][1] && mat[1][1]==mat[2][2]) //diagonally from left to right
			{
				res=1;
				System.out.println("Winner:"+mat[1][1]);
			}
			if(res==0)
			{
				if(mat[0][2]!=0 && mat[1][1]!=0 && mat[2][0]!=0 && mat[0][2]==mat[1][1] && mat[1][1]==mat[2][0]) //diagonally from right to left
				{
					res=1;
					System.out.println("Winner:"+mat[1][1]);
				}
			}
		}
		return res;
	}
	void ticTacToe()  //main algo of tic-tac-toe
	{
		int flag=0;
		int turn=0;
		while(flag==0) //play untill anyone wins or draw 
		{
			int isWin=isWin();
			int isDraw=isDraw();
			if(isWin==1 || isDraw==1)
			{
				if(isDraw==1 && isWin==0)
				{
					System.out.println("Draw!!!!");
				}
				flag=1;
			}
			else
			{
				if(turn%2==0)   //if even turn the user will play
				{
					userTurn();
					System.out.println("===User===");
					displayMat(mat);
				}
				else            //otherwise i.e Odd turn Computer play
				{
					machineTurn();
					System.out.println("===Machine===");
					displayMat(mat);
				}
				turn++;
			}
			
		}
		
	}
	void machineTurn()      //how machine will apply its intelligent i.e code for machine where to put its symbol
	{
		int noOfZero=calculateEmptyTile();          //calculate no of zeros(black space) in card
		
		
		int tileTwoSame=isTwoTileSameSame();        //check if any two tiles are same or not
		if(tileTwoSame==0)                          // if no then
		{
			int macMat[][]=emptyTileIndex(noOfZero);   //machine wil enter its symbol accoding to MIN-MAX algorithm
			copyMachineInputToMat(macMat);
		}
	
	}
	void copyMachineInputToMat(int temp[][])  //copy a temp matrix to original card or matrix
	{
		for(int i=0;i<3;i++)
		{
			for(int j=0;j<3;j++)
			{
				mat[i][j]=temp[i][j];
			}
		}
	}
	int calculateEmptyTile( )  //it will calulate empty tiles in card
	{
		int res=0;
		for(int i=0;i<3;i++)
		{
			for(int j=0;j<3;j++)
			{
				if(mat[i][j]==0)
				{
					res++;
				}
			}
		}
		return res;
	}
	int[][] copyMat(int temp[][])
	{
		int tempMat[][]=new int[3][3];
		for(int i=0;i<3;i++)
		{
			for(int j=0;j<3;j++)
			{
				tempMat[i][j]=temp[i][j];
			}
		}
		return tempMat;
	}
	int isTwoTileSameSame() //return 1 if any two tiles are same
	{
		int res=0;
		for(int i=0;i<3;i++)
		{
			if(mat[i][0]!=0 && mat[i][1]!=0 && mat[i][0]==mat[i][1] && mat[i][2]==0 )  //row 
			{
				res=1;
				//System.out.println("mat["+i+"][2]=2");
				mat[i][2]=2;
				break;
			}
			if(mat[i][1]!=0 && mat[i][2]!=0 &&   mat[i][1]==mat[i][2] && mat[i][0]==0) //column
			{
				res=1;
				//System.out.println("mat["+i+"][0]=2");
				mat[i][0]=2;
				break;
			}
			if(mat[i][0]!=0 && mat[i][2]!=0 && mat[i][0]==mat[i][2] && mat[i][1]==0) //row 
			{
				res=1;
				//System.out.println("mat["+i+"][1]=2");
				mat[i][1]=2;
				break;
			}
			if(mat[0][i]!=0 && mat[1][i]!=0 && mat[0][i]==mat[1][i] && mat[2][i]==0) //column
			{
				res=1;
				//System.out.println("mat[2]["+i+"]=2");
				mat[2][i]=2;
				break;
			}
			if(mat[1][i]!=0 && mat[2][i]!=0  && mat[1][i]==mat[2][i] && mat[0][i]==0) // column
			{
				res=1;
				//System.out.println("mat[0]["+i+"]=2");
				mat[0][i]=2;
				break;
			}
			if(mat[0][i]!=0 && mat[2][i]!=0 && mat[0][i]==mat[2][i] && mat[1][i]==0) //column
			{
				res=1;
				//System.out.println("mat[1]["+i+"]=2");
				mat[1][i]=2;
				break;
			}
			
		}
		if(res==0 && mat[0][0]!=0 && mat[1][1]!=0 && mat[0][0]==mat[1][1] && mat[2][2]==0)  //diagonally
		{
			res=1;
			//System.out.println("mat[2][2]=2");
			mat[2][2]=2;
		}
		if(res==0 && mat[1][1]!=0 && mat[2][2]!=0 && mat[1][1]==mat[2][2] && mat[0][0]==0 ) //diagonally
		{
			res=1;
			//System.out.println("mat[0][0]=2");
			mat[0][0]=2;
		}
		if(res==0 && mat[0][0]!=0 && mat[2][2]!=0 && mat[0][0]==mat[2][2] && mat[1][1]==0) //diagonally
		{
			res=1;
			//System.out.println("mat[1][1]=2");
			mat[1][1]=2;
		}
		if(res==0 && mat[0][2]!=0 && mat[1][1]!=0 && mat[0][2]==mat[1][1] && mat[2][0]==0) //diagonally
		{
			res=1;
			//System.out.println("mat[2][0]=2");
			mat[2][0]=2;
		}
		if(res==0 && mat[1][1]!=0 && mat[2][0]!=0 &&  mat[1][1]==mat[2][0] && mat[0][2]==0 ) //diagonally
		{
			res=1;
			//System.out.println("mat[0][2]=2");
			mat[0][2]=2;
		}
		if(res==0 && mat[0][2]!=0 && mat[2][0]!=0 && mat[0][2]==mat[2][0] && mat[1][1]==0) //diagonally
		{
			res=1;
			//System.out.println("mat[1][1]=2");
			mat[1][1]=2;
		}
		return res;
		
	}
	int[][] emptyTileIndex(int noOfZero)// find empty tile and return the next Max Matrix whose (e) value is max 
	{
		int i=0;
		int j=0;
		//PriorityQueue<MyComparator> pq=new PriorityQueue();
		int max=Integer.MIN_VALUE;
		int visited[][]=new int[3][3];
		int finalMat[][]=new int[3][3];
		
		//mark visited[i][j]=1 where number are already placed
		
		for(int k=0;k<3;k++)
		{
			for(int l=0;l<3;l++)
			{
				if(mat[k][l]!=0)
				{
					visited[k][l]=1;
				}
			}
		}
		
			int k=0;
			while(k<noOfZero)
			{
				int myMat[][]=copyMat(mat);
				int flag=0;
				for(i=0;i<3;i++)
				{
					for(j=0;j<3;j++)
					{
						if(visited[i][j]==0)
						{
							if(myMat[i][j]==0)
							{
								flag=1;
								visited[i][j]=1;
								break;
							}
						}
					}
					if(flag==1)
					{
						break;
					}
				}
				
				myMat[i][j]=2;
				int PossWin_X=possibilityOfWinX(myMat);
				int possWin_Y=possibilityOfWinY(myMat);
				int e=PossWin_X-possWin_Y;
				if(e>max)
				{
					finalMat=copyMat(myMat);
				}
				//pq.add(new MyComparator(myMat, e));
				k++;
			}
		
		return finalMat;
		
	}
	void userTurn() /user turn
	{
		System.out.println("where you want to insert "+userSymbol);
		System.out.println("position of i:");
		i=sc.nextInt();
		System.out.println("position of j:");
		j=sc.nextInt();
		mat[i][j]=userSymbol;
	}
	int isDraw()  //check is their draw or not
	{
		int res=0;
		int k=0;
		come:for(int i=0;i<3;i++)
		{
			if(mat[i][0]!=0 && mat[i][1]!=0 && mat[i][2]!=0)
			{
				k++;
				continue come;
			}
		}
		if(k==3)
		{
			res=1;
		}
		return res;
	}
  
  
  
  
	int possibilityOfWinY(int mat[][])  //calculate possibily of Computer winning
 	 {
		int res=0;
		int flag=0;
		for(int i=0;i<3;i++)
		{
			flag=0;
			for(int j=0;j<3;j++)
			{
				if(mat[i][j]==1)
				{
					flag=1;
					break;
				}
			}
			if(flag==0)
			{
				res++;
			}
		}
		
		for(int j=0;j<3;j++)
		{
			flag=0;
			for(int i=0;i<3;i++)
			{
				if(mat[i][j]==1)
				{
					flag=1;
					break;
				}
			}
			if(flag==0)
			{
				res++;
			}
		}
		int j=0;
		flag=0;
		for(int i=0;i<3;i++,j++)
		{
			if(mat[i][j]==1)
			{
				flag=1;
				break;
			}
		}
		if(flag==0)
		{
			res++;
		}
		j=2;
		flag=0;
		for(int i=0;i<3;i++,j--)
		{
			if(mat[i][j]==1)
			{
				flag=1;
				break;
			}
		}
		if(flag==0)
		{
			res++;
		}
		
		return res;
	}
	int possibilityOfWinX(int mat[][])  //calculate possibily of User winning
	{
		int res=0;
		int flag=0;
		for(int i=0;i<3;i++)
		{
			flag=0;
			for(int j=0;j<3;j++)
			{
				if(mat[i][j]==2)
				{
					flag=1;
					break;
				}
			}
			if(flag==0)
			{
				res++;
				//System.out.println("Row x:"+res);
			}
		}
		
		for(int j=0;j<3;j++)
		{
			flag=0;
			for(int i=0;i<3;i++)
			{
				if(mat[i][j]==2)
				{
					flag=1;
					break;
				}
			}
			if(flag==0)
			{
				res++;
				//System.out.println("column x:"+res);
			}
		}
		int j=0;
		flag=0;
		for(int i=0;i<3;i++,j++)
		{
			if(mat[i][j]==2)
			{
				flag=1;
				break;
			}
		}
		if(flag==0)
		{
			res++;
			//System.out.println("diagonal 1 x:"+res);
		}
		j=2;
		flag=0;
		for(int i=0;i<3;i++,j--)
		{
			if(mat[i][j]==2)
			{
				flag=1;
				break;
			}
		}
		if(flag==0)
		{
			res++;
			//System.out.println("diagonal 2:"+res);
		}
		
		return res;
	}
  
	void displayMat(int mat[][])  //diplay card of tic-tac-toe
	{
		for(int i=0;i<3;i++)
		{
			for(int j=0;j<3;j++)
			{
				System.out.print(mat[i][j]+" ");
			}
			System.out.println();
		}
	}
	public static void main(String args[])
	{
		MainClass m=new MainClass();
		
		m.getData();
		
		System.out.println("===Initial Board===");
		m.displayMat(m.mat);
		
		m.ticTacToe();
	
		
	}

}
