C++ Mini-Game 🎮✨
A fun and interactive mini-game built with C++, featuring engaging mechanics and smooth gameplay. This project showcases my skills in game logic, user input handling, and efficient programming techniques. A step forward in my coding journey, blending creativity with problem-solving! 🚀



#include <iostream>
#include <cstring>

using namespace std;

// -------------------- PLAYER CLASS --------------------
class Player 
{
    char name[50];
    int keys;  // Keeps track of collected keys

public:
    Player() 
    {
        keys = 0;
    }
    void getData();
    void startGame();
    void collectKey();
    bool hasKey();
};

void Player::getData() 
{
    cout<<"Welcome!!! Let's Start The Game.\n All The Best."<<endl;
    cout << "ENTER THE PLAYER NAME: \n";
    cin.ignore();
    cin.getline(name, 50);
}

void Player::startGame() 
{
    cout << "\nThe door locks behind you... The air turns cold...\n";
    cout << "Welcome to your nightmare. Will you escape?\n";
}

void Player::collectKey() 
{
    keys++;
    cout << "You found a key! Total keys: " << keys << endl;
}

bool Player::hasKey() 
{
    return keys > 0;
}

// -------------------- ROOM CLASS --------------------
class Room 
{
public:
    virtual void findClue() = 0;
    virtual bool solveRiddle() = 0;
    virtual void unlock() = 0;
};

// -------------------- TUTORIAL ROOM --------------------
class TutorialRoom : public Room 
{
    string riddle1, riddle2, riddle3, riddle4;
public:
    void findClue();
    bool solveRiddle();
    void unlock();
};

void TutorialRoom::findClue() 
{
    cout << "\n--- TUTORIAL ROOM ---\n";
    cout << "You wake up in a strange room. There's a note...\n";
}

bool TutorialRoom::solveRiddle() 
{
    string answer;
    cout << "\nRiddle 1: I speak without a mouth and hear without ears. What am I?\n ";
    cin >> answer;
    if (answer != "echo") return false;
    cout << "\nRiddle 2: The more of this there is, the less you see. What is it? \n";
    cin >> answer;
    if (answer != "darkness") return false;
    cout << "\nRiddle 3: I have keys but open no locks. What am I? \n";
    cin >> answer;
    if (answer != "keyboard") return false;
    cout << "\nRiddle 4: What comes once in a minute, twice in a moment, but never in a thousand years? \n";
    cin >> answer;
    return answer == "m";
}

void TutorialRoom::unlock() 
{
    cout << "The door unlocks. A key falls into your hand!\n";
}

// -------------------- DINING HALL --------------------
class DiningHall : public Room 
{
public:
    void findClue();
    bool solveRiddle();
    void unlock();
};

void DiningHall::findClue() 
{
    cout << "\n--- DINING HALL ---\n";
    cout << "You enter a dimly lit dining hall...\n";
}

bool DiningHall::solveRiddle() 
{
    string answer;
    cout << "\nRiddle 1: I have teeth but never bite. What am I? \n";
    cin >> answer;
    if (answer != "knife") return false;
    cout << "\nRiddle 2: I'm small and white but make your food taste better. What am I? \n";
    cin >> answer;
    if (answer != "salt") return false;
    cout << "\nRiddle 3: I can light up the night or destroy all in sight. What am I? \n";
    cin >> answer;
    if (answer != "fire") return false;
    cout << "\nRiddle 4: I hold your food, but I'm not a dish. What am I? \n";
    cin >> answer;
    return answer == "plate";
}

void DiningHall::unlock() 
{
    cout << "A hidden compartment reveals a key!\n";
}

// -------------------- LABORATORY --------------------
class LaboratoryRoom : public Room 
{
public:
    void findClue();
    bool solveRiddle();
    void unlock();
};

void LaboratoryRoom::findClue() 
{
    cout << "\n--- LABORATORY ---\n";
    cout << "You enter a futuristic-looking laboratory...\n";
}

bool LaboratoryRoom::solveRiddle() 
{
    string answer;
    cout << "\nRiddle 1: What is 3/7 chicken, 2/3 cat, and 2/4 goat? \n";
    cin >> answer;
    if (answer != "chicago") return false;
    cout << "\nRiddle 2: Multiply this number by any other number, and it remains the same. What is it? \n";
    cin >> answer;
    if (answer != "zero") return false;
    cout << "\nRiddle 3: What has many rings but no fingers? \n";
    cin >> answer;
    if (answer != "phone") return false;
    cout << "\nRiddle 4: I sometimes run, but I can't walk. What am I? \n";
    cin >> answer;
    return answer == "nose";
}

void LaboratoryRoom::unlock() 
{
    cout << "A final key is revealed... You are free to leave!\n";
}

// -------------------- MAIN FUNCTION --------------------
int main() 
{
    Player player;
    player.getData();
    player.startGame();

    // Tutorial Room
    TutorialRoom tutorial;
    tutorial.findClue();
    while (!tutorial.solveRiddle()) 
    {
        cout << "Wrong answer! Try again.\n";
    }
    tutorial.unlock();
    player.collectKey();

    // Dining Hall
    if (player.hasKey()) 
    {
        DiningHall dining;
        dining.findClue();
        while (!dining.solveRiddle()) 
        {
            cout << "Wrong answer! Try again.\n";
        }
        dining.unlock();
        player.collectKey();
    }

    // Laboratory Room
    if (player.hasKey()) 
    {
        LaboratoryRoom lab;
        lab.findClue();
        while (!lab.solveRiddle()) 
        {
            cout << "Wrong answer! Try again.\n";
        }
        lab.unlock();
    }

    cout << "\nCONGRATULATIONS! YOU HAVE ESCAPED THE NIGHTMARE!\n";
    return 0;
}
