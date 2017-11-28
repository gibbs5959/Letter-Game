# Letter-Game
User guesses letter from file 

//Brandaija Gibbs
//10/6/2017
//Large Program 1: Letter Game


#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <ctype.h>
#define MAXGUESSES 5


//PROTOTYPES
void GameRules();
void GuessTheLetter(char);
char GetTheGuess(int);
int	CompareLetters(char, char);

//MAIN FUNCTION //MAIN FUNCTION //MAIN FUNCTION
int main()
{
	//First Declare Variables
	char letter, lowletter; //store letter from file, lowercase letter from file
	int numGames, i; //user inputted number of games, starting number??
	i = 0;
	//Find the file aka DECLARE FILE POINTER & connect to it
	FILE*intPtr;
	intPtr = fopen("letterList.txt", "r");

	//Next, greet the user and explain the game 
	GameRules();

	//Now, ask and get the number of games to play
	printf("How many games would you like to play?");
		scanf("%d", &numGames);
	

	//CREATE A LOOP ALLOWS USER TO PLAY MORE THAN ONE GAME 
	for (i = 0; i < numGames; i=i+1)
	{
		printf("\n\n\n\nXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n\n");
		printf("Ready to play game %d!\n\n", i+1);
		printf("-------------------------------");
		//get a solution letter from file - use fscanf
		fscanf(intPtr, " %c", &letter);
		//change the solution to lowercase
		lowletter = tolower(letter);
		//call the GuessTheLetter function and pass it the solution
		GuessTheLetter(lowletter);
	}

	//close file pointer
	return 0;
}

//FUNCTION DEFINITIONS

//greets the user and explain the game 
void GameRules()
{
	printf("Hello! Welcome to the Letter Guessing Game!\n\n\n");
	printf("Here is how you play:\n");
	printf("For each game you will have 5 chances to guess each letter.\n Let's begin.\n\n");
	printf("First, you will enter the number of games you want to play, from 1-8.\n\n\n");
}

void GuessTheLetter(char solutionfromfile) //plays one round of game. needs to Gettheguess from user and Comparetheletters
{
	//arg1 is the letter from the solution (lowletter)
	int numGuesses = 1, win = 0, numGames = 0; 
	char guess, guesslower, solution;
	solution = solutionfromfile;

	//set condition to play game up to max number of guesses
	while (numGuesses <= MAXGUESSES && win == 0)
	{
		//starts to get the guess and compareeltters
		guess = GetTheGuess(numGuesses);//get a guess from the user
		guesslower = tolower(guess); //change the guess to lowercase 
		win = CompareLetters(guesslower, solution); 
		numGuesses++; // count the number of guesses so far 
	}

	//use conditons to let user know wheter they won or lost round of game
	if (win == 1)
	{
		printf("You have won the game!\n\n The solution and the guess are the same :)\n\n",guess);
		numGames = 1 + numGames;
		return ;
	}
	else if (win != 1)
	{
		printf("Sorry you lost this round :(\n\n");
		return ;
	}
	return ;
}

char GetTheGuess(int numGuesses)
{
	char guess1;
	printf("\nGetting guess number %d.\n\n", numGuesses);
	printf("Enter a guess.\n");
	scanf(" %c", &guess1);
	return guess1;
}

int CompareLetters(char playerguess, char fileletter)
{
	if (playerguess == fileletter)
	{
	return 1;
	}
		
	else if (playerguess > fileletter)
	{
		printf("The solution comes before your letter (%c).\n\n", playerguess);
		return 0;
	}
		
	else if (playerguess < fileletter) 
	{
	printf("The solution comes after your letter (%c).\n\n", playerguess);
	return 0;
	}
	
}
