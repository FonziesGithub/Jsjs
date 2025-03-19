# Jsjs

#include <iostream>
#include <string>

using namespace std;

// Struct for quiz questions
struct QuizItem {
    string tagalogWord;  // Array column 1
    string choices[3];   // Array column 2
    char correctAnswer;  // Array column 3
};

// Struct for storing player data
struct Player {
    string name;
    int score;
};

// Function for displaying a border
void Border() {
    cout << "------------------------------\n";
}

// Opening greeting and instructions
void OpeningGreeting() {
    cout << "Welcome to Translation: (Tagalog to English) QUIZ\n"
         << "Answer in uppercase letters only and no special characters.\n"
         << "Type your answers and press Enter to submit.\n\n";
}

// Function for conducting the quiz
void ConductQuiz(QuizItem quiz[], int size, Player& player) {
    char answer;
    player.score = 0;

    // Main loop for questions
    for (int i = 0; i < size; i++) {
        Border();
        cout << "Question number " << i + 1 << endl;
        cout << "Translate the following Tagalog word into English: " << quiz[i].tagalogWord << endl;

        // Loop for displaying choices (A, B, C)
        for (int j = 0; j < 3; j++) {
            cout << quiz[i].choices[j] << endl;
        }

        cout << "Your answer: ";
        cin >> answer;
        answer = toupper(answer);  // Convert user input to uppercase
        Border();

        // Conditional to check the answer
        if (answer == quiz[i].correctAnswer) {
            cout << "Correct!\n";
            player.score++;  // Increment the player's score
        } else {
            cout << "Wrong! The correct answer is " << quiz[i].correctAnswer << ".\n";
        }
        system("pause");
        system("cls");
    }
}

// Function for displaying individual results
void DisplayResults(const Player& player) {
    Border();
    cout << player.name << " got a score of: " << player.score << "/10\n";
    if (player.score == 10) {
        cout << "Grade: A (Very Good)\n";
    } else if (player.score >= 7) {
        cout << "Grade: B (Good)\n";
    } else {
        cout << "Grade: F (Failed)\n";
    }
    Border();
}

// Function for displaying all results
void DisplayAllResults(const Player players[], int count) {
    cout << "Final Results:\n";
    Border();
    for (int i = 0; i < count; i++) {
        DisplayResults(players[i]);
    }
}

// Function for choosing whether to continue
bool Choose(char& opt) {
    do {
        cout << "Do you want to continue? yes [y] or no [n]: ";
        cin >> opt;
        opt = tolower(opt);

        if (opt == 'y') {
            return true;
        } else if (opt == 'n') {
            exit(0);
        } else {
            cout << "Invalid input. Please try again.\n";
        }
        system("cls");
    } while (true);
}

// Main function
int main() {
    const int MAX_PLAYERS = 5, MAX_QUESTIONS = 10;
    Player players[MAX_PLAYERS];
    int playerCount;
    char option;

    QuizItem quiz[MAX_QUESTIONS] = {
        {"Umaga", {"A) morning", "B) night", "C) afternoon"}, 'A'},
        {"Mahusay", {"A) bad", "B) okay", "C) good"}, 'C'},
        {"Dalubhasa", {"A) noob", "B) expert", "C) hacker"}, 'B'},
        {"Bayani", {"A) villain", "B) antagonist", "C) hero"}, 'C'},
        {"Kutsilyo", {"A) knife", "B) spoon", "C) fork"}, 'A'},
        {"Hagdan", {"A) roof", "B) stairs", "C) door"}, 'B'},
        {"Bahay", {"A) house", "B) building", "C) garage"}, 'A'},
        {"Salamat", {"A) gracias", "B) merci", "C) thanks"}, 'C'},
        {"Pitaka", {"A) wallet", "B) card", "C) pocket"}, 'A'},
        {"Salapi", {"A) bands", "B) stack", "C) cash"}, 'C'}
    };

    // Continuous loop until the specified number of players completes
    do {
        cout << "How many players are playing? (Max: 5): ";
        cin >> playerCount;

        if (playerCount <= 0 || playerCount > MAX_PLAYERS) {
            cout << "Invalid number of players. Please enter a number between 1 and 5.\n";
            continue;
        }

        for (int i = 0; i < playerCount; i++) {
            Border();
            cout << "Enter player " << i + 1 << "'s name: ";
            cin.ignore();
            getline(cin, players[i].name);
            OpeningGreeting();
            Border();

            ConductQuiz(quiz, MAX_QUESTIONS, players[i]);
        }

        DisplayAllResults(players, playerCount);
        system("pause");
        system("cls");

    } while (Choose(option));

    return 0;
}
