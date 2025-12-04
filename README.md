Assignment 2 - Objective 1 — Understand the Existing Game Logic

Overview This is a simple console-based obstacle avoidance game written in C for Windows. The player controls a character that can move left or right across three lanes to avoid falling obstacles. The game also includes background music and collision sound effects.

Game Components

Player Represented by the character 6. Moves left (LEFT arrow) and right (RIGHT arrow) across three lanes (0, 1, 2). Position stored in variable x.

Obstacle Represented by the character 1. Moves vertically from top to bottom of the screen. Lane randomly selected each cycle (obstaclePos = rand() % 3). Vertical position tracked by step (0 to 10).

Screen The game uses a 10-row track plus one row for the player. To reduce flickering, the console cursor is reset to the top (clear_screen_fast()) instead of clearing the screen with system("cls").

Sound Background music (bg.wav) plays in a loop. Collision triggers a sound effect (impact.wav). Uses PlaySound from <mmsystem.h>.

Game Flow

Initialization Set console color with system("color 4F"). Start background music asynchronously. Initialize random seed for obstacle lane generation. Set initial player lane (x = 1) and initial obstacle lane (obstaclePos = rand() % 3).

Main Loop Runs indefinitely until collision occurs.

a. Input Handling Uses _kbhit() to detect keypress without blocking. Arrow keys move the player left or right.

b. Drawing the Screen Uses clear_screen_fast() to move cursor to the top to reduce flicker. Prints track with obstacles at the current step. Draws player at the bottom row in the current lane.

c. Collision Detection If the obstacle reaches the player's row (step == 10) and the player is in the same lane (x == obstaclePos), collision occurs: Stops background music. Plays collision sound. Waits 2.5 seconds (Sleep(2500)) and prints GAME OVER!.

d. Obstacle Movement Increment step to move the obstacle down. If step > 10, reset step = 0 and choose a new lane for the obstacle.

Timing The game loop has Sleep(120) to control the speed of the obstacle falling.

Implementation Details

Screen Refresh: clear_screen_fast() uses Windows API SetConsoleCursorPosition for smoother screen updates. This is better than system("cls") as it reduces flickering.

Random Obstacles: The lane of each obstacle is randomized for unpredictability.

Collision Logic: Only checks collision when the obstacle reaches the player row.

Audio Handling: Plays background music asynchronously to avoid blocking the game loop.

Observations

Strengths Smooth console refresh reduces flicker. Simple, easy-to-understand logic. Works with basic Windows-only C functions for sound and console handling.

Potential Improvements Add multiple obstacles simultaneously. Add player vertical movement for a more dynamic game. Implement score tracking based on avoided obstacles. Add difficulty levels by increasing obstacle speed over time. Use cross-platform libraries for portability (e.g., SDL, ncurses).

Objective 2 — Implement Modifications -

I added 4 things in this game -

Modifications done -

Assignment 3 -

Objective — Develop Your Own Game -

Typing Game Game Idea

The Typing Game is a simple console-based game where the player must type displayed words correctly before they reach the bottom of the screen. The game challenges typing speed and accuracy while increasing difficulty as the player progresses through levels.


Rules-

Score System
Player Lives
Difficulty Levels
Multiple Obstacles
A simple console-based **Quiz Game written in C language**.  
The game allows the user to select a difficulty level (number of questions) and displays the final score at the end.

---

## 📁 About the Project

This project demonstrates:
- Use of **conditional statements**
- **Loops** and **switch-case logic**
- **User input handling**
- **Basic scoring system**
- **Structured program design**

The player selects a mode:
| Mode | Questions |
|------|-----------|
| 1 | 5 Questions |
| 2 | 10 Questions |
| 3 | 15 Questions |

After answering all questions, total score is displayed.

---

## 🚀 Features
✔ Multiple choice questions  
✔ Three different levels (5, 10, 15 questions)  
✔ Score calculation  
✔ Beginner-friendly C code  
✔ Runs on any C compiler (Turbo C, GCC, Online GDB, Dev C++, CodeBlocks)

---

## 🛠 Technologies Used
- C Programming Language
- Standard Input/Output

---

## 🧾 How to Run the Program

### **Using GCC**
```bash
