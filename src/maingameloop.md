# Main Game Loop
## Main Game Loop 
Infinite Loop that only exists when the game is quit. The loop:
1. Handles Input
2. Updating Game
3. Rendering

## Game State System
Used to organize close of different states of games into their own classes. The main game loop calls these functions in a stack like way. Once all the states have been popped, the game will close. 
