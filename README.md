# Code-Breaker
// Code Breaker
//Nicholas Buckley 10.21.2018

#include "pch.h"
#include <iostream>
#include <string>
#include <cstdlib>
#include <ctime>

using namespace std;

int main()
{
	int words, finish, attempts; 
	char again; // To ask the user to play again
	enum fields { WORD, HINT, NUM_FIELDS };
	const int NUM_WORDS = 10; // Amount of words created
	const string WORDS[NUM_WORDS][NUM_FIELDS] = // Creating an array with the words and hints
	{
		// List of all words and hints 
		{"apple", "Doesn't fall far from the tree."},
		{"boat", "It floats on water."},
		{"truck", "Comes to pick up your trash."},
		{"bottle", "Holds liquids for you."},
		{"hat", "Goes on your head."},
		{"gum", "You can blow bubbles with this."},
		{"candle", "Makes your house smell nice."},
		{"flag", "Is at the top of a pole."},
		{"mouse", "Likes to eat cheese."},
		{"phone", "You can text and call with this."}
	}; //ends array

	//Welcomes user and explaines games
	cout << "\t\t\tWelcome to Code Breaker!\n\n";
	cout << "Unscramble the letters to make a word.\n";
	cout << "Enter 'hint' for a hint.\n";
	cout << "Enter 'quit' to quit the game.\n";
	cout << "You will be asked to solve three different codes.\n";
	cout << "Good Luck!\n";
	
	do // do statement to continue playing
	{
		words = 0; // To track the number of words solved
		finish = 3; // The amount of words needed to finish the game
		do // do statement to reach 3 words
		{
			attempts = 1; // To track the number of tries it takes the user
			
			srand(static_cast<unsigned int>(time(0))); // allowing the creation of a random number
			int choice = (rand() % NUM_WORDS); // The random number that selects the word
			string theWord = WORDS[choice][WORD];  // The word that has been selected
			string theHint = WORDS[choice][HINT];  // The hint relating to the word

			string jumble = theWord;  // the jumbled version of the word selected
			int length = jumble.size(); // calculating the length of the word
			for (int i = 0; i < length; ++i) // jumbling the letters of the word based off the length of the word
			{
				int index1 = (rand() % length);
				int index2 = (rand() % length);
				char temp = jumble[index1];
				jumble[index1] = jumble[index2];
				jumble[index2] = temp;
			}
			cout << "====================================================================================================================\n";
			cout << "\nThe code is: " << jumble; // display the jumbled word

			string guess; // create the users guess
			cout << "\n\nYour guess: ";
			cin >> guess; // input the users guess
			attempts++;

			while ((guess != theWord) && (guess != "quit")) // loop that continues while user is incorrect or quits
			{
				if (guess == "hint") // if statement to display the word hint
				{
					cout << theHint;
					attempts = (attempts - 1);

				}
				else // else in if statements shows incorrect answer
				{
					cout << "Sorry, that's not it.\n";
					cout << "Enter hint for assistants or quit to end the simmulation.";
				}

				cout << "\n\nYour guess: ";
				cin >> guess;
				attempts++; //increase user attempt count
			}

			if (guess == theWord) // If the user guesses the correct answer
			{
				cout << "\nThat's it!  You guessed it!\n";
				++words; // increase number of words finished
				attempts++;//increases user attempt count
			}

		} while (words != finish); // Ends statement once user finished three words
		
		cout << "====================================================================================================================\n";
		cout << "You have succesfully finished three codes with " << attempts << " guesses.\n";
		cout << "\nWould you like to play again? Y/N: "; // Ask user to play again
		cin >> again; // record user input

	} while (again == 'Y'); // if input is Y user will play again

	cout << "\nThanks for playing.\n";

	return 0;
}
