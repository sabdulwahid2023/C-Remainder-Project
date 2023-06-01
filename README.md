# C-Remainder-Project

#include <iostream>
#include <string>
#include <random>
#include <ctime>

using namespace std;

// Takes the greatest common divisor of both the numerator and denominator
// and returns the remainder of the denominator and numerator.

int gcd(int num1, int num2)
{
    if (num1 == 0)
        return num2;

    return gcd(num2 % num1, num1);
}

// Used to simplify the fraction by taking a common factor by
// using the gcd function. It passes by reference the numerator and denominator.

void simplifyFraction(int& numer, int& denom)
{

    int comFactor = gcd(numer, denom);

    denom = denom / comFactor;
    numer = numer / comFactor;
}

// Function computer uses to divide both fractions by multiplying
// the numerator of the first fraction by denominator of second fraction and
// the numerator of the second fraction by denominator of first fraction.

void divide(int numer1, int numer2, int denom1, int denom2, int& resultNumer, int& resultDenom)
{
    resultNumer = (numer1 * denom2);

    resultDenom = (denom1 * numer2);

    simplifyFraction(resultDenom, resultNumer);
}

// Function computer uses to multiply both fractions by multiplying
// the numerator of the first fraction by numerator of second fraction and
// the denominator of the second fraction by denominator of first fraction.

void multiply(int numer1, int numer2, int denom1, int denom2, int& resultNumer, int& resultDenom)
{
    resultNumer = (numer1 * numer2);

    resultDenom = (denom1 * denom2);

    simplifyFraction(resultDenom, resultNumer);
}

// Generates a random - generated number from the computer in the range
// 1-9.

void genFraction(int& numerator, int& denominator)
{
    numerator = (rand() % 9) + 1;

    denominator = (rand() % 9) + 1;

}

// Allows the user to enter an input in the x/y form or just x.
// Utilizes a do while loop to check if input consists of a front slash or
// newline.

void userInput(int& userNumer, int& userDenom)
{
    char newChar;
    cin >> userNumer;

    do
    {
        newChar = cin.get();
    } while (newChar != '/' && newChar != '\n');

    if (newChar == '/')
    {
        cin >> userDenom;
        
    }
}

// Displays the menu.

void Displaymenu()
{

    cout << "\tFraction Quizlet Menu" << endl;
    cout << endl;
    cout << "\t1 - Multiplication quiz" << endl;
    cout << "\t2 - Division quiz" << endl;
    cout << "\t3 - Quit program" << endl;
    cout << endl;

}

// Displays the problem by taking "a" (counter that is iterated through the for
// loop) and the numerators and denominators as well as the character literal
// for the operation.

void displayProblem(int a, int numer1, int denom1, int numer2, int denom2, char operation)
{
    cout << endl;
    cout << "Question #" << a << ": What is the result of the following?" << endl;
    //Display Question
    cout << endl;
    cout << "  " << numer1 << "       " << numer2 << endl;
    cout << "-----" << " " << operation << " " << "-----" << endl;
    cout << "  " << denom1 << "       " << denom2 << endl;
    cout << endl;
    cout << "Enter the answer in the form x / y or just x: ";
    //cout << endl;

}

// Displays the answer when the user enters an incorrect answer. Passes the
// numerators and denomiators of both function plus the numerator and denominator
// of the answer of computer as well as the character literal operation.

void displayAnswer(int numer1, int denom1, int numer2, int denom2, int resultNumer, int resultDenom, char operation)
{
    if(resultDenom == 1)
    {
        cout << "  " << numer1 << "       " << numer2 << "       " << endl;
        cout << "-----" << " " << operation << " " << "-----" << " " << "=" << " " << resultNumer << endl;
        cout << "  " << denom1 << "       " << denom2 << "       " << endl;
        cout << endl;
    }
    
    // displaying the answer

    else
    {
        cout << "  " << numer1 << "       " << numer2 << "        " << resultNumer << endl;
        cout << "-----" << " " << operation << " " << "-----" << " " << "=" << " " << "------" << endl;
        cout << "  " << denom1 << "       " << denom2 << "        " << resultDenom << endl;
        cout << endl;
    }
}

int main()
{
    unsigned int seed;

    seed = time(0);
    srand(seed);

    int numerator1 = 0, denominator1 = 0, numerator2 = 0, denominator2 = 0;

    int userNumer, userDenom, resultNum, resultDenom, whichChoice;

    int count = 0;

    char whichOperation;

    const int MULTIPLICATION = 1;
    const int DIVISION = 2;
    const int QUIT = 3;

    do
    {
        Displaymenu();

        cout << "Enter the number of your choice: ";
        cin >> whichChoice;
        //cout << endl;

        switch (whichChoice)
        {
        // if computer-generated denominator is equal to 1
        case MULTIPLICATION:

            count = 0;

            for (int i = 1; i < 6; i++)
            {
                // Defining and initializing all the variables

                genFraction(numerator1, denominator1);
                genFraction(numerator2, denominator2);
                whichOperation = '*';

                displayProblem(i, numerator1, denominator1, numerator2, denominator2, whichOperation);
                

                userInput(userNumer, userDenom);

                multiply(numerator1, numerator2, denominator1, denominator2, resultNum, resultDenom);
                
                // comparing the user entered by the user and generated
                // by the computer.

                if ((userNumer == resultNum) && (userDenom == resultDenom))
                {
                    cout << endl;
                    cout << "That is correct!";
                    count++;
                    cout << endl;
                    
                }
                else if (userDenom == 1)
                {
                    cout << endl;
                    cout << "That is incorrect." << endl;
                    cout << endl;
                    displayAnswer(numerator1, denominator1, numerator2, denominator2, resultNum, resultDenom, whichOperation);
                }
                else
                {
                    cout << endl;
                    cout << "That is incorrect." << endl;
                    cout << endl;
                    displayAnswer(numerator1, denominator1, numerator2, denominator2, resultNum, resultDenom, whichOperation);
                }
            }
                
            // conditions for displaying a message based on the value of the
            // counter.
                
            if (count < 4)
            {
                cout << endl;
                cout << "You need more practice." << endl;
                cout << "You got " << count << " of " << "5 problems correct." << endl;
                cout << endl;
                cout << endl;
            }
            else if (count == 4)
            {
                cout << endl;
                cout << "Outstanding work!" << endl;
                cout << "You got 4 of 5 problems correct." << endl;
                cout << endl;
                cout << endl;
            }
            else
            {
                cout << endl;
                cout << "Outstanding work!" << endl;
                cout << "You got 5 of 5 problems correct." << endl;
                cout << endl;
                cout << endl;
            }
            break;

        case DIVISION:

            count = 0;

            for (int i = 1; i < 6; i++)
            {
                // Defining and initializing all the variables

                genFraction(numerator1, denominator1);
                genFraction(numerator2, denominator2);
                whichOperation = '/';

                displayProblem(i, numerator1, denominator1, numerator2, denominator2, whichOperation);
                
                

                userInput(userNumer, userDenom);

                divide(numerator1, numerator2, denominator1, denominator2, resultNum, resultDenom);
                
                
                // comparing the user entered by the user and generated
                // by the computer.
                
                if ((userNumer == resultNum) && (userDenom == resultDenom))
                {
                    cout << endl;
                    cout << "That is correct!" << endl;
                    count++;
                    cout << endl;
                }
                else if (userDenom == 1)
                {
                    cout << endl;
                    cout << "That is incorrect." << endl;
                    cout << endl;
                    displayAnswer(numerator1, denominator1, numerator2, denominator2, resultNum, resultDenom, whichOperation);
                }
                else
                {
                    cout << endl;
                    cout << "That is incorrect." << endl;
                    cout << endl;
                    displayAnswer(numerator1, denominator1, numerator2, denominator2, resultNum, resultDenom, whichOperation);
                    //cout << endl;
                }
            }
            
            // conditions for displaying a message based on the value of the
            // counter.
                
            if (count < 4)
            {
                cout << endl;
                cout << "You need more practice." << endl;
                cout << "You got " << count << " of " << "5 problems correct." << endl;
                cout << endl;
                cout << endl;
            }
            else if (count == 4)
            {
                cout << endl;
                cout << "Outstanding work!" << endl;
                cout << "You got 4 of 5 problems correct." << endl;
                cout << endl;
                cout << endl;
            }
            else
            {
                cout << endl;
                cout << "Outstanding work!" << endl;
                cout << "You got 5 of 5 problems correct." << endl;
                cout << endl;
                cout << endl;
            }
            break;

        case QUIT:
            break;
        default:
            cout << endl;
            cout << "Invalid menu choice entered." << endl;
            cout << endl;

        }
    } while (whichChoice != 3);

    return 0;
}
