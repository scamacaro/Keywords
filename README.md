# Keywords
Assigmnet Keywords
/*
Sanyerlis Camacaro- CSC215 - Sancamac@uat.edu
Assignment: Keywords - Building Code Breaker Training Simulation Program for CIA Recruits.
"Functions"

I've been hired as a coder for the CIA, and I've been assigned to code a simple Code Breaker
Training Simimulation Program for CIA Recruits called Keywords.

To create a Code Breaker Training Simulation Program that gives user directions and tell 
how to break the code.
*/

#include "pch.h" // includes precompiled header, faster to process for the compiler. 
#include <iostream> // includes input and out as the standard library.
#include <string> // this includes and allows me to work with strings.
#include <cstdlib> // general utilities.
#include <ctime> // converts the time value pointed to by time to local time as string. 

using namespace std;// means using standard namespace and that I dont have to type std:: in front of each line.
string Name; // declares Name as string instruction.

int main() // first line of your program, your first instruction.
{
	
	cout << "\tCode Breaker Training Simulation Program for CIA Recruits\n" << endl; // Title of Program 
	cout << "Enter your name: "; // Asks user to input their name
	cin >> Name; // user inputs recruit's name and the name is displayed throughout the simulation. 
	// Display an overview of the Simulation Program and displays recruit's name. 
	cout << "\nWelcome to the Code Breaker Training Simulation Program " << ",Recruit," << Name << "!\n";
	cout << "You will be decoding multiple Enemies Secrets.\n\n"; // tells users that they will be decoding multiple words.
	// Display an directions to the recruit on how to use Keywords
	cout << "Rectruit, " << Name << " your task is to code break the scramble words secrets.\n"; // giving the recruit instructions.
	cout << "\nYou will guess letters that are secret words to prevent future attacks to the CIA!\n"; // giving the recruit instructions.

	char playAgain = 'y'; // declares the function playAgain when user inputs 'y' as chracter type variables.

	while (playAgain == 'y') // if user inputs 'y' the program restarts. 
	{
		// enum adds a number for the amount of fields. So it gets the word, the hint and gets the number of fields.
		enum fields { WORD, HINT, NUM_FIELDS };
		// Sets a boundary for rows to 10.
		const int NUM_WORDS = 10;
		// Creates a constant string array where rows is 5 and columns is calculated by NUM_FIELDS which is 2
		const string WORDS[NUM_WORDS][NUM_FIELDS] =
		{
			// Initializes the array with the WORD and then the HINT.
			{"code", "Program instructions."}, // word 1.
			{"programming", "Running instructions in order."}, // word 2.
			{"function", "kind of rule that, for one input, it gives one output."}, // word 3.
			{"command", "An order or the authority to command."}, // word 4.
			{"pointer", "A variable that stores the memory address as its value."}, // word 5.
			{"include", "Header file in C++."}, // word 6.
			{"strings", "C-Style character _____ originated within the C language."}, // word 7.
			{"simulation", "Imitation of a situation or process."}, // word 8.
			{"cout", "Object of class ostream in C++."}, // word 9.
			{"arrays", "A collection of elements of placed in the same type in contiguous memory locations."} // word 10.
		};

		srand(static_cast<unsigned int>(time(nullptr)));// Seeds the random number generator to time.

		int attempts = 0;// Keeps track of how many attempts the player has tried to unscramble the code.
		int correct = 0;// Keeps track of how many times the word was correct.
		int hintsUsed = 0;// Keeps track of how many hints the recruit had to use.
		string guess;// Keeps track of the users guess.


		// Congratulates the agent on becoming part of the team and gives instructions to unscramble secret code. 
		cout << Name << ", Congratulations on becoming part of the team of the C.I.A.\n"; // congratulates agent. 
		cout << "\t\t\t\tOur enemy has outsmarted our technology by using single scrambled low-tech keywords.\n"; // enemy message.
		cout << "\t\t\t\tAll you have to do here, is unscramble the secret word.\n" << endl; // direction to user.
		cout << "\t\t\t\t\t\tEnter 'hint' for a hint.\n"; // directions for hint.
		cout << "\t\t\t\t\t\tEnter 'quit' to quit the game.\n\n"; // directions for quitting the game.

	
		while (correct < 3) // Enter the game loop, less than 3 tries.
		{
			
			int playerChoice = (rand() % NUM_WORDS);// Makes choice a random number within the amount of NUM_WORDS.
			string codeWord = WORDS[playerChoice][WORD]; // The word to guess.
			string codeHint = WORDS[playerChoice][HINT]; // The hint for the word to guess.

			string jumble = codeWord; // Jumbled version of the selected word "codeWord.
			int length = jumble.size(); // Gets the size of the word to jumble and sets it to an integer called length.
			for (int i = 0; i < length; i++) // loop keeps its execution until one of its elements are a null element.
			{
				// index1 and index2 generates two random positions and swaps characters at those positions.
				int index1 = (rand() % length);
				int index2 = (rand() % length);
				char temp = jumble[index1];
				jumble[index1] = jumble[index2];
				jumble[index2] = temp;
			}

			
			while (guess != codeWord)// Nested while loop so the player can keep guessing the word without it doing the main loop and changes the word.
			{
				cout << "The Secret Word is: " << jumble; // tells user what is the secret word
				cout << "\n\nYour guess: "; // asks for user guess for secret word. 
				cin >> guess;// user inputs their guess for secret word. 

				if (guess == "hint") // calls the function when user enter hint.
				{
					cout << codeHint << "\n\n"; // message that displays for hint.
					hintsUsed++; // keeps score of how many times hint was used.
				}
				else if (guess == "quit") // calls the function for quit.
				{
					cout << "Thank you for trying, come back when you're ready...\n\n" << endl; // message that displays when user quits.
					return 0; // if successful returns value. 
				}
				else if (guess == codeWord) // calls the function when user enters the correct word. 
				{
					cout << "Correct!\n\n"; // displays message that it's correct.
					correct++; // keeps score of how many corrects.
					attempts++; // keeps score of how many attempts.
				}
				else // if not correct calls this function. 
				{
					cout << "Sorry, that's not the secret word.\n\n"; // displays this message is user input is not correct.
					attempts++; // keeps score of attempts. 
				}
			}
		}

		// Displays the stats to the user. Uses an if else if statement.
		cout << "\nTraining complete.\n\n"; // message displayed for user.
		cout << "\t\t\tYour stats:\n"; // message displayed for user.
		
		if ((attempts == correct) && (hintsUsed == 0)) // if all attempts and no hints were used calls this function
		{
			cout << "Out of " << attempts << " attempts you got " << correct << " right.\n"; // tells user how many correct attempts they got.
			cout << "You're doing a Great as CIA, you used " << hintsUsed << " hints."; // tells user how many times they used hints.
		}
		else if (attempts == correct) // calls function is correct
		{
			cout << "Out of " << attempts << " attempts you got " << correct << " right. Great job!\n"; // tells user how many correct attempts.
			cout << "You also used " << hintsUsed << " hints."; // tells user how many hints they used.
		}
		else if (attempts >= (correct + 3)) // function when attempts are wrong for more than 3 times.
		{
			// tells the user how many attemps they got correct.
			cout << "Out of " << attempts << " attempts you got " << correct << " right. You need to retry again soon...\n";
			cout << "You also used " << hintsUsed << " hints."; // tells the user how many hints they used.
		}
		else // function to tell the user how many they got correct
		{
			cout << "Out of " << attempts << " attempts you got " << correct << " right.\n";// tells the user how many attemps they got correct.
			cout << "You also used " << hintsUsed << " hints.";// tells the user how many hints they used.
		}

		
		cout << "\n\nDo you want to play again? (y/n): "; // Starts the process to play the simulation again if the user chooses to.
		cin >> playAgain; // user input to play again. 
		cout << "\n\n"; // extra line.
	}

	return 0;// if successful returns value. 
}
