#include <iostream>
using namespace std;

char b[3][3] = {{'1','2','3'},{'4','5','6'},{'7','8','9'}};
string p1, p2;
char turn = 'X';
int score1 = 0, score2 = 0;

void show() {
    for(int i=0; i<3; i++){
        for(int j=0; j<3; j++)
            cout << b[i][j] << " ";
        cout << endl;
    }
}

bool win() {
    for(int i=0; i<3; i++)
        if(b[i][0]==b[i][1] && b[i][1]==b[i][2]) return true;
    for(int i=0; i<3; i++)
        if(b[0][i]==b[1][i] && b[1][i]==b[2][i]) return true;
    if(b[0][0]==b[1][1] && b[1][1]==b[2][2]) return true;
    if(b[0][2]==b[1][1] && b[1][1]==b[2][0]) return true;
    return false;
}

void reset() {
    char num='1';
    for(int i=0; i<3; i++)
        for(int j=0; j<3; j++)
            b[i][j]=num++;
}

void menu() {
    cout << "1. Play Game\n";
    cout << "2. View Rules\n";
    cout << "3. Exit\n";
}

void rules() {
    cout << "Tic Tac Toe Rules:\n";
    cout << "* 3x3 grid\n";
    cout << "* X starts\n";
    cout << "* Match 3 in a row/column/diagonal to win\n";
}

int main() {
    cout << "Player 1 name: ";
    cin >> p1;
    cout << "Player 2 name: ";
    cin >> p2;

    int choice;
    while(true){
        menu();
        cin >> choice;
        if(choice == 1){
            reset();
            turn = 'X';
            score1 = score2 = 0;
            bool play=true;
            while(play){
                for(int i=0; i<9; i++){
                    show();
                    cout << (turn=='X' ? p1 : p2) << "'s turn. Enter position: ";
                    int pos;
                    cin >> pos;
                    if(pos < 1 || pos > 9){
                        cout << "Invalid position!\n";
                        i--;
                        continue;
                    }
                    int r=(pos-1)/3, c=(pos-1)%3;
                    if(b[r][c]!='X' && b[r][c]!='O'){
                        b[r][c] = turn;
                        if(win()){
                            show();
                            cout << (turn=='X' ? p1 : p2) << " Wins 🎉\n";
                            if(turn == 'X') score1++;
                            else score2++;
                            break;
                        }
                        turn = (turn=='X')?'O':'X';
                    }
                    else i--;
                }
                if(!win()) cout << "Draw Game\n";
                cout << p1 << ": " << score1 << " | " << p2 << ": " << score2 << endl;
                cout << "Play again? (1/0): ";
                cin >> play;
            }
        }
        else if(choice == 2) rules();
        else if(choice == 3) break;
        else cout << "Invalid choice!\n";
    }
    return 0;
}
