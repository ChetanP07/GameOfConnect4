
import java.util.*;
class GameOfConnect4
{
    public static void main(String[] args)
    {
        Scanner sc=new Scanner(System.in);
        System.out.println("Enter the size of the board :");
        int n=sc.nextInt();
        int m=sc.nextInt();
        System.out.println("Enter the series of pieces :");
        int p=sc.nextInt();
        int y=n*m;
        char[][] board=new char[n][m];
        
        //initializing the array
		for (int row = 0; row < board.length; row++){
			for (int col = 0; col < board[0].length; col++){
				board[row][col] = ' ';
			}
		}

        int turn = 1;
        char player = 'R';
        boolean winner = false;
        int x = board.length/2;
        
        //Playing the turn
        while(winner==false && turn<=y)
        {
            boolean validPlay;
            int play;
            do
            {
                display(board);
                System.out.println("Player "+player+" choose the column:");
                play=sc.nextInt();

                validPlay=valid(play,board);

            }while(validPlay==false);

            //marking the column
            for(int row=board.length-1;row>=0;row--)
            {
                if(board[row][play]==' ')
                {
                    board[row][play]=player;
                    break;
                }
            }
            //To find the winner 
            winner=Winner(p,player,board);

            //switch players
			if (player == 'R'){
				player = 'B';
			}else{
				player = 'R';
			}
			
			turn++;	

        }
        display(board);

        if (winner){
			if (player=='R'){
				System.out.println("Blue won");
			}else{
				System.out.println("Red won");
			}
		}else{
			System.out.println("Tie game");
		}
    }
        //Displaying the board
        public static void display(char[][] board){
             
            System.out.println("---------------");
            for (int row = 0; row < board.length; row++){
                System.out.print("|");
                for (int col = 0; col < board[0].length; col++){
                    System.out.print(board[row][col]);
                    System.out.print("|");
                }
                System.out.println();
                System.out.println("---------------");
            }
            
            System.out.println();
        }
        
        //Checking the Invalid key and board IsFull 
        public static boolean valid(int column, char[][] board){
            //valid column?
            if (column < 0 || column > board[0].length){
                return false;
            }
            
            //full column?
            if (board[0][column] != ' '){
                return false;
            }
            
            return true;
        }

        //Checking the Winner
        public static boolean Winner(int p,char player ,char [][]board)
        {   
            int x = board.length/2;
            
            //Checking the combination horizontally
            for(int row=0;row<board.length;row++)
            {
                int piece=0;
                for(int col=0;col<board[0].length;col++)
                {
                    
                    if(board[row][col]==player)
                    {
                        piece=piece+1;
                        if(piece==p)
                        {
                            System.out.println("Congratulation Player "+player+" has Won the game" );
                            return true;
                        }
                    }
                    else
                    {
                        piece=0;
                    }
                }
            }

            //Checking the combination vertically 
            for(int col=0;col<board[0].length;col++)
            {
                int piece=0;
                for(int row=0;row<board.length;row++)
                {
                    
                    if(board[row][col]==player)
                    {
                        piece=piece+1;
                        if(piece==p)
                        {
                            System.out.println("Congratulation Player "+player+" has Won the game" );
                            return true;
                        }
                    }
                    else
                    {
                        piece=0;
                    }
                }
            }

            //Checking upward diagonally
            for(int row=x;row<board.length;row++)
            {
                int piece=0;
                for(int col=0;col<board[0].length-x;col++)
                {
                    if(board[row][col]==player)
                    {
                        piece=piece+1;
                        if(piece==p)
                        {
                            System.out.println("Congratulation Player "+player+" has Won the game" );
                            return true;
                        }
                    }
                    else
                    {
                        piece=0;
                    }
                }
            }

            //Checking downward diagonally
            for(int row=0;row<board.length-x;row++)
            {
                int piece=0;
                for(int col=0;col<board[0].length-x;col++)
                {
                    if(board[row][col]==player)
                    {
                        piece=piece+1;
                        if(piece==p)
                        {
                            System.out.println("Congratulation Player "+player+"has Won the game" );
                            return true;
                        }
                    }
                    else
                    {
                        piece=0;
                    }
                }
            }
            return false;
        }


    
}
