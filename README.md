# gtech1-b17-pong
c'est un pong
#include <stdio.h>
#define NBL 6
#define NBC 7

int player = 1 ;
int end = 0;

char tab[NBL][NBC];

char tokens[] = "ox";

void testhorizontal(void){
  for (int i = 0 ; i < NBL ; i++){
    for (int j = 3 ; j < NBC ; j++){
      if (tab[i][j-3] == tokens[player] && tab[i][j-2] == tokens[player] && tab[i][j-1] == tokens[player] && tab[i][j] == tokens[player]){
        printf("well played player : %d\n" , player);
        end = 42 ;
      }
    }
  }
}

void testvertical(void){
  for (int i = 0 ; i < NBL ; i++){
    for (int j = 3 ; j < NBC ; j++){
      if (tab[j-3][i] == tokens[player] && tab[j-2][i] == tokens[player] && tab[j-1][i] == tokens[player] && tab[j][i] == tokens[player]){
        printf("well played player : %d\n" , player);
        end = 42 ;
      }
    }
  }
}

void testdiagonal1(void){
  for (int i = 3 ; i < 6 ; i++){
    for (int j = 0 ; j < 4 ; j++){
      if (tab[i][j] == tokens[player] && tab[i-1][j+1] == tokens[player] && tab[i-2][j+2] == tokens[player] && tab[i-3][j+3] == tokens[player]){
        printf("well played player : %d\n" , player);
        end = 42 ;
      }
    }
  }
}

void testdiagonal2(void){
  for (int i = 0 ; i < 3 ; i++){
    for (int j = 0 ; j < 4 ; j++){
      if (tab[i][j] == tokens[player] && tab[i+1][j+1] == tokens[player] && tab[i+2][j+2] == tokens[player] && tab[i+3][j+3] == tokens[player]){
        printf("well played player : %d\n" , player);
        end = 42 ;
      }
    }
  }
}

void affiche(void){
    printf("-------------\n");
    for(int l = 0; l < NBL;l++){
      for(int c = 0; c < NBC;c++){
        printf("%c ", tab[l][c]);
      }
    printf("\n");
    }
  printf("-------------\n");
}

void init(void){
    for(int l = 0; l < NBL;l++){
      for(int c = 0; c < NBC;c++){
        tab[l][c] = '.';
      }
    }
}

int main(void){

  int column = 7;
  int row = 5;
  int columnFilled[7] = {0,0,0,0,0,0,0};
  init();
  printf("Welcome to Connect 4\n");
  while (end < 42){
    if(player == 1){
      player--;
    }
    else if(player == 0){
      player++;
    }
    affiche();
          while ((column < 1 || column > 7 ) || column == 7 || columnFilled[column-1] == 1){
            if(columnFilled[column-1] == 1){
              printf("Column full try another one !\n");
            }
            printf("[Player %d] choose a column : " , player);
            scanf("%d",&column);
          }
          if (tab[0][column-1] == '.'){
            for(int row = 5;row > -1;row--){
              if (tab[row][column-1] == '.'){
                tab[row][column-1] = tokens[player];
                break;
              }
              if (row == 1){
                columnFilled[column-1] = 1;     
              }
            }
          }    
        column = 7;
        end++;
        testvertical();
        testdiagonal1();
        testdiagonal2();
        testhorizontal();
  }
  affiche();
}
