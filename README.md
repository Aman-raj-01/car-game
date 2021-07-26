//car_game_Project
#include<iostream>
#include<conio.h>
#include<dos.h>
#include<windows.h>
#include<time.h>
//this is a define headers
#define SCREEN_WIDTH 90
#define SCREEN_HEIGHT 26
#define WIN_WIDTH 70

using namespace std;

HANDLE console = Getstdhandle (STD_OUTPUT_HANDLE );
COORD cursorposition;

int enemyY[3];
int enemyX[3];
int enemyFlag[3];
char car [4][4] = {'','±','±','',
                   '±','±','±','±',
                   '','±','±','',
                   '±','±','±','±'};
                   '±','±','±','±'};
                   
int carPos = WIN_WIDTH/2;
int score = 0;

void gotoxy (int X, int Y){
  cursorposition.X = X;
  cursorposition.Y = Y;
  setconsolecursorposition(console, cursorposition);
}
void setcursor(bool visible, DWORD size) {
  if(size == 0)
     size = 20;
     
     CONSOLE_CURSOR_INFO lpCursor;
     lpCursor.bvisible = visible;
     lpcCursor.dwsize = size;
     setconsolecursorInfo(console,&lpcCursor);
}
void drawBorder(){
  for(int i=0; i<SCREEN_HEIGHT; i++ ){
    for(int j=0; j<17; j++ ){
      gotoxy(0+j,i);cout<<"±";
      gotoxy(WIN_WIDTH-j,i); cout<<"±";
  }
  
}
for(int i=0; i<SCREEN_HEIGHT; i++ ){
  gotoxy(SCREEN_WIDTH,i); cout<<"±";
}
//block
}
void genEnemy(int ind){
  enemyX[ind] = 17 + rand()%(32);
}
void drawEnemy(int ind){
  if(enemyFlag[ind] == true ){
    gotoxy(enemyX[ind], enemyY[ind]); cout<<"****";
    gotoxy(enemyX[ind], enemyY[ind]+1); cout<<" ** ";
    gotoxy(enemyX[ind], enemyY[ind]+2); cout<<"****";
    gotoxy(enemyX[ind], enemyY[ind]+3); cout<<" ** ";
  }
  void eraseEnemy(int ind){
  if(enemyFlag[ind] == true ){
    gotoxy(enemyX[ind], enemyY[ind]); cout<<"  ";
    gotoxy(enemyX[ind], enemyY[ind]+1); cout<<"  ";
    gotoxy(enemyX[ind], enemyY[ind]+2); cout<<"  ";
    gotoxy(enemyX[ind], enemyY[ind]+3); cout<<"  ";
}
void resetEnemy(int ind){
  eraseEnemy(ind)
  enemyY[ind] = 1;
  genEnemy(ind);
  
}
void drawCar(){
  for(int i=0; i<4; i++){
    for(int j=0; j<4; j++)
    gotoxy(j+carPos, i+22); cout<<car[i][j];
       }
   }
}
void eraseCar(){
  for(int i=0; i<4; i++){
    for(int j=0; j<4; j++)
    gotoxy(j+carPos, i+22); cout<<car[i][j];
       }
   }
}
int collision(){
  if(enemyY[0]+4 >= 23){
    if(enemyX[0] + 4 - carPos >= 0 && enemyX[0] + 4 - carPos >9 ){
      
      return 1;
    }
  }
  return 0;
  
}
int gameover(){
  system ("cls");
  cout<<endl;
  cout<<"\t\t---------------------"<<endl;
  cout<<"\t\t------GAME OVER------"<<endl;
  cout<<"\t\t---------------------"<<endl;
  cout<<"\t\t press any key to go back the menu";
  getch();
}
void updateScore(){
  gotoxy(WIN_WIDTH + 7, 5);cout<<"Score: "<<Score<<endl;
}
void instruction(){
  
  system ("cls");
  cout<<"instruction";
  cout<<"\n--------------";
  cout<<"\n Avoid car by moving left or right";
  cout<<"\n\n Press 'a' to move left ";
  cout<<"\n Press 'd' to move right";
  cout<<"\n Press 'Escape' to exit ";
  cout<<"\n\n Press any key to go back the menu";
  getch();
}
void play(){
  carPos = -1, WIN_WIDTH/2;
  Score = 0;
  enemyFlag[0] = 1;
  enemyFlag[1] = 0;
  enemyY[0] = enemyY[1] = 1;
  
  system("cls");
  drawBorder();
  updateScore();
  genEnemy(0);
  genEnemy(1);
  
  gotoxy(WIN_WIDTH + 7, 2);cout<<"car game";
  gotoxy(WIN_WIDTH + 6, 4);cout<<"--------";
  gotoxy(WIN_WIDTH + 6, 6);cout<<"--------";
  gotoxy(WIN_WIDTH + 7, 12);cout<<"control";
  gotoxy(WIN_WIDTH + 7, 13);cout<<"------";
  gotoxy(WIN_WIDTH + 2, 14);cout<<" A key - Left";
  gotoxy(WIN_WIDTH + 2, 15);cout<<" D key - Right";
  
  //that is a car game.
  
  gotoxy(18, 5);cout<<"Press any key to start";
  gotoxy();
  gotoxy(18, 5);cout<<"             ";
  
  while(1){
    if (kbhit()){
      char ch = getch();
      if (ch=='a' || ch=='A'){
        /*this is a seeing*/
        if(carPos < 50)
           carpos += 4;
      }
      if (ch==27){
        break;
      }
    }
    drawCar();
    drawEnemy(0);
    drawEnemy(1);
    if(collision() == 1 ){
      gameover();
      return;
    }
    Sleep(50);
    eraseCar();
    eraseEnemy(0);
    eraseEnemy(1);
    
    if( enemyY[0] == 10 )
        if ( enemyFlag[1] == 0 )
           enemyFlag[1] == 1;
           
           if ( enemyFlag[0] == 1 )
           enemyFlag[0] += 1;
             if ( enemyFlag[1] == 1 )
           enemyFlag[1] += 1;
           
           if(enemyY[0] > SCREEN_HEIGHT-4){
              resetEnemy[0];
              Score++;
              updateScore();
           }
          if(enemyY[1] > SCREEN_HEIGHT-4){
              resetEnemy[1];
              Score++;
              updateScore();
           } 
  }
}
int main()
{
  setcursor(0,0);
  srand((unsigned)time(NULL));
  do {
    system("cls");
    gotoxy(10,5); cout<<"----------------";
    gotoxy(10,6); cout<<"| 🚘🚔🚗CAR GAME🚘🚔🚗 |";
    gotoxy(10,7); cout<<"----------------";
    gotoxy(10,9); cout<<"1.Start Game";
    gotoxy(10,10); cout<<"2.Instruction";
    gotoxy(10,11); cout<<"3. Quit";
   gotoxy(10,13); cout<<" SELECT OPTION: ";
   char op = getche();
   
   if (op=='1') play();
   else if (op=='2') instruction();
   else if (op=='3') exit(0);
  }while(1);
  
  return 0;
}
