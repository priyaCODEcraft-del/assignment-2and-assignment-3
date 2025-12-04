#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <windows.h>
#include <conio.h>

#define LANES 3
#define TRACK_ROWS 10
#define MAX_OBSTACLES 6

typedef struct {
    int lane;
    int row;
    int active;
} Obstacle;

void clear_screen_fast(void) {
    HANDLE h = GetStdHandle(STD_OUTPUT_HANDLE);
    COORD pos = {0, 0};
    SetConsoleCursorPosition(h, pos);
}

void set_cursor_visible(int visible) {
    HANDLE hOut = GetStdHandle(STD_OUTPUT_HANDLE);
    CONSOLE_CURSOR_INFO cci;
    GetConsoleCursorInfo(hOut, &cci);
    cci.bVisible = visible ? TRUE : FALSE;
    SetConsoleCursorInfo(hOut, &cci);
}

void init_obstacles(Obstacle obs[], int n) {
    for (int i = 0; i < n; i++) obs[i].active = 0;
}

void spawn_obstacle(Obstacle obs[], int n) {
    for (int i = 0; i < n; i++) {
        if (!obs[i].active) {
            obs[i].active = 1;
            obs[i].lane = rand() % LANES;
            obs[i].row = 0;
            return;
        }
    }
}

void clear_all_obstacles(Obstacle obs[], int n) {
    for (int i = 0; i < n; i++) obs[i].active = 0;
}

int main(void) {
    system("color 0A");
    srand((unsigned int)time(NULL));
    int playerLane = 1;
    int score = 0;
    int lives = 3;
    int level = 1;
    int speed = 140;
    const int minSpeed = 50;
    Obstacle obstacles[MAX_OBSTACLES];
    init_obstacles(obstacles, MAX_OBSTACLES);
    set_cursor_visible(0);
    spawn_obstacle(obstacles, MAX_OBSTACLES);
    spawn_obstacle(obstacles, MAX_OBSTACLES);

    while (1) {
        clear_screen_fast();

        if (_kbhit()) {
            int ch = _getch();
            if (ch == 0 || ch == 224) ch = _getch();
            if (ch == 75 && playerLane > 0) playerLane--;
            else if (ch == 77 && playerLane < 2) playerLane++;
            else if (ch == 27) break;
        }

        level = score / 5 + 1; // fix: level purely from score

        printf(" SCORE: %d   LIVES: %d   LEVEL: %d\n", score, lives, level);
        printf("|--- --- ---|\n");
        for (int row = 0; row < TRACK_ROWS; row++) {
            char laneChar[LANES] = {' ', ' ', ' '};
            for (int i = 0; i < MAX_OBSTACLES; i++)
                if (obstacles[i].active && obstacles[i].row == row)
                    laneChar[obstacles[i].lane] = 'X';
            printf("| %c   %c   %c |\n", laneChar[0], laneChar[1], laneChar[2]);
        }

        if (playerLane == 0) printf("| P         |\n");
        else if (playerLane == 1) printf("|     P     |\n");
        else printf("|         P |\n");

        int hit = 0;
        for (int i = 0; i < MAX_OBSTACLES; i++)
            if (obstacles[i].active && obstacles[i].row == TRACK_ROWS - 1 && obstacles[i].lane == playerLane) {
                hit = 1;
                obstacles[i].active = 0;
            }

        if (hit) {
            lives--;
            clear_all_obstacles(obstacles, MAX_OBSTACLES);
            playerLane = 1;
            Sleep(800);
            if (lives <= 0) {
                clear_screen_fast();
                printf("GAME OVER!\n");
                printf("Final Score: %d\n", score);
                printf("Final Level: %d\n", level);
                break;
            }
        }

        Sleep(speed);

        for (int i = 0; i < MAX_OBSTACLES; i++)
            if (obstacles[i].active) obstacles[i].row++;

        for (int i = 0; i < MAX_OBSTACLES; i++)
            if (obstacles[i].active && obstacles[i].row >= TRACK_ROWS) {
                obstacles[i].active = 0;
                score++;
                if (speed > minSpeed) speed -= 2; 
            }

        int activeCount = 0;
        for (int i = 0; i < MAX_OBSTACLES; i++) if (obstacles[i].active) activeCount++;
        if (activeCount < level + 1 && rand() % 3 == 0) spawn_obstacle(obstacles, MAX_OBSTACLES);
    }

    set_cursor_visible(1);
    printf("\nPress any key to exit...");
    _getch();
    return 0;
}
