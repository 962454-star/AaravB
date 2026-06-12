# Hi, I'm Aarav Batua
Welcome to my ICS4U portfolio. I’ll use this site to post my work and reflections.

## Highlights
- 🔧 Project 1 (Currently in progress): *Researching Physical Health Issues That Stem From Computer Use* – *Combining medicine and computer usage by tying orthopedic physical health issues with increased screen time*
- 🧠 Concept I learned: *(in progress)*
- 📝 Blog/Reflection: *(in progress)*

## About me

❤️‍🩹 A third-year high school student and Cricketer

👀 A keen interest in Medicine, Cricket, Self-Improvement, and Dharma

🔗 "You have a right to perform your prescribed duties, but you are not entitled to the fruits of your actions. Never consider yourself to be the cause of the results of your activities, nor be attached to inaction." ―Bhagwan Krishna, Bhagavad Gita 2.47"

## Extracurricular Activities

### (2023-Present) The Hindu Student Association, Port Credit Secondary School, Mississauga, ON
*The President*
- Leading a 6-member executive team to operate one of the school’s largest cultural clubs, engaging 35–40 active members weekly.
- Developing interactive educational activities, such as Jeopardy-style sessions on Sanatan Dharma, strengthening cultural understanding, and boosting recurring participation.
- Strengthening cross-club and staff relationships, positioning HSA for multi-club collaborations and higher cultural visibility across campus.

### (2024-Present) The Varsity Cricket Team PCSS, Port Credit Secondary School, Mississauga, ON
*Captain, Top-order, One-down batsman* 
- Captaining the varsity team to a 100% win rate, implementing strategic field placements, adaptive batting orders, and disciplined in-game coordination.  
- Anchoring one down, absorbing pressure, neutralizing opposition spells, and dictating innings tempo through high-value shot selection.  
- Fostering team cohesion in a culturally diverse squad, collaborating with teammates from India, Pakistan, Afghanistan, and beyond to maximize performance and unity.  
- Modeling high-performance discipline through rigorous fitness, focus, and preparation standards on and off the field.

### (2024-Present) Health Occupations Students of America (HOSA), Toronto, Ontario
*Pathophysiology Category Competitor*
- Competing against 7,000+ high school and university students
- Participating in hands-on workshops learning skills such as Suturing
- Learning from research-based seminars hosted by medical-school graduates, surgeons, and etc.

### (2024-2025) The SciTech Student Council, Port Credit Secondary School, Mississauga, ON
*Grade 10 Representative*

- Represented 119 Grade 10 SciTech students, serving as primary liaison to council leadership and administration.  
- Expanded school-wide STEM engagement by promoting the Science Fair to students beyond the SciTech program.  
- Secured $400+ in sponsorship funding from local organizations, supporting event logistics and expanding resources for student initiatives.  
- Supported planning and execution of programming for 509 students, contributing to logistics, communication, and event engagement.

### Daily Log Final Project 

Day 1
Code For Monday:
a) The concepts I implemented today were variables and data-tracking. My entire session
was spent on planning and mostly declaring all the variables the game would need
before writing any of my logic. These are some of the variables that would be extremely
significant to my game, especially the boolean ones. I identified three types that I
completely needed, which are the boolean, int and int. I also added two PImage
variables for the two players that will play the game.
b) I grouped the variables into five categories based on their planned roles in the game.
The float group is gonna cover everything physics-related, like playerSize, runSpeed,
jumpForce, and etc. The velocity variables are all floats because physics calculations
produce decimal values. Gravity was planned as 0.4 and an int cannot store that, and
velocity is accumulating in tiny increments, since p1Vy += 0.4 each frame, those
decimals compound over time for the smooth jump I am planning to build.
c) The main challenge today was deciding the correct type for variables where it wasn't
immediately obvious. The one I was debating on using was startMillis. I knew I needed to
track when a round starts to calculate the countdown timer, and millis in Processing
returns a whole number in milliseconds, so int was the right choice. I had to think
carefully about whether float precision was needed for timing. I decided whole
milliseconds were precise enough for a 30-second round timer. Another challenge was
planning the tagging variables ahead of writing any collision logic. I hadn't yet written
checkTagContacts() but I knew from thinking through the game logic that two players
overlapping would cause rapid role-swapping every frame without a cooldown, so I had
to create a cooldown as soon as possible.
Day 2
Day 2 Code:
/ Images
PImage playerR, playerP;
// Player Properties
float playerSize = 35;
float runSpeed = 5;
float jumpForce = -10;
float gravity = 0.4;
// Player 1 State
float p1X, p1Y;
float p1Vy = 0;
boolean p1OnGround = false;
// Player 2 State
float p2X, p2Y;
float p2Vy = 0;
boolean p2OnGround = false;
// Game Control
boolean isP1It = true;
int p1Score = 0;
int p2Score = 0;
int totalTime = 30;
int timeRemaining;
int startMillis;
boolean gameOver = false;
int gameState = 0; // 0 = Main Menu, 1 = Playing, 2 = Game Over
// Tagging Systems
int lastTagMillis = 0;
int tagCooldown = 1000; // 1 second of immunity before another tag can happen
// Input Trackers for arrow keys and wasd
boolean p1Left, p1Right, p1Jump;
boolean p2Left, p2Right, p2Jump;
void setup() {
size(1000, 562);
drawMainMenu();
keyPressed();
}
void drawMainMenu() {
background(255, 235, 100); // Bright Yellow Background
textAlign(CENTER, CENTER);
fill(0);
textSize(50);
text("2D PLATFORM TAG", width/2, height/2 - 100);
textSize(20);
fill(50);
text("P1: W, A, D | P2: Arrow Keys", width/2, height/2 - 30);
// Draw Clickable "PLAY" Button
rectMode(CENTER);
stroke(0);
strokeWeight(3);
fill(240, 210, 50); // Darker yellow to differentiate
rect(width/2, height/2 + 70, 200, 60, 10);
// Play Button Text
noStroke();
fill(0);
textSize(24);
text("PLAY", width/2, height/2 + 70);
}
void mousePressed() {
// If we are on the menu screen, check if the player clicked the PLAY button bounding
box
if (gameState == 0) {
if (mouseX > width/2 - 100 && mouseX < width/2 + 100 && mouseY > height/2 + 40
&& mouseY < height/2 + 100) {
gameState = 1; // Change state to Gameplay
}
}
}
void keyPressed() {
if (gameState == 1) { // Only track movement keys during playing state, to be worked
on further using our boolean logic tomorrow
if (key == 'a' || key == 'A') p1Left = true;
if (key == 'd' || key == 'D') p1Right = true;
if (key == 'w' || key == 'W') p1Jump = true;
if (key == CODED) {
if (keyCode == LEFT) p2Left = true;
if (keyCode == RIGHT) p2Right = true;
if (keyCode == UP) p2Jump = true;
}
}
}
a) Today I added selection structures to my game. I used if statements to control
which screen the game displays, detect whether the player clicked the play
button, and restrict key input to only work during gameplay. The central tool
driving most of this was the gameState variable that I added, an int that will hold
0 for the mina menu, 1 for the playing state of the entire game (main one), and 2
for game over.
b) I tried using selection structures in three places today, each solving a different
problem. First I upgraded boolean gameOver to int gameState. A boolean only
represents two states, running or over, but I need three screens, a main menu
screen at the starting was also required. A boolean cannot express three states,
so I replaced it with an int, and as explained earlier, now I know which screen
should be active, this will be very important for our game later on. The second
was the button detection in mousePressed(). The outer if statement checks if
gameState is 0, and if the player isn’t on the main menu, the click does nothing.
The inner if statement checks whether the mouse coordinates fall inside the play
button’s rectangle. If the click lands inside those bounds, then the game state will
change to 1, turning on playing mode. The last thing is keyPressed. This adds
most of the input logic required when our game will be running when gameState
is 1.
c) The main challenge was designing the bounding box check correctly. The play
button is drawn using rectMode(CENTER), meaning the X and Y passed to rect()
refer to its center point, not a corner. My first attempt at click detection used the
center coordinates directly as the boundary limits, which produced a detection
zone offset from the actual button. I fixed it by calculating the edges manually
and subtracting and adding half the width and height from the center so the
detection zone matched exactly what was drawn on screen.
Day 3
// Images
PImage playerR, playerP;
// Player Properties
float playerSize = 35;
float runSpeed = 5;
float jumpForce = -10;
float gravity = 0.4;
// Player 1 State
float p1X, p1Y;
float p1Vy = 0;
boolean p1OnGround = false;
// Player 2 State
float p2X, p2Y;
float p2Vy = 0;
boolean p2OnGround = false;
// Game Control
boolean isP1It = true;
int p1Score = 0;
int p2Score = 0;
int totalTime = 30;
int timeRemaining;
int startMillis;
boolean gameOver = false;
int gameState = 0; // 0 = Main Menu, 1 = Playing, 2 = Game Over
// Tagging Systems
int lastTagMillis = 0;
int tagCooldown = 1000; // 1 second of immunity before another tag can happen
// Input Trackers for arrow keys and wasd
boolean p1Left, p1Right, p1Jump;
boolean p2Left, p2Right, p2Jump;
void setup() {
size(1000, 562);
drawMainMenu();
keyPressed();
}
void drawMainMenu() {
background(255, 235, 100); // Bright Yellow Background
textAlign(CENTER, CENTER);
fill(0);
textSize(50);
text("2D PLATFORM TAG", width/2, height/2 - 100);
textSize(20);
fill(50);
text("P1: W, A, D | P2: Arrow Keys", width/2, height/2 - 30);
// Draw Clickable "PLAY" Button
rectMode(CENTER);
stroke(0);
strokeWeight(3);
fill(240, 210, 50); // Darker yellow to differentiate
rect(width/2, height/2 + 70, 200, 60, 10);
// Play Button Text
noStroke();
fill(0);
textSize(24);
text("PLAY", width/2, height/2 + 70);
}
void mousePressed() {
// If we are on the menu screen, check if the player clicked the PLAY button bounding
box
if (gameState == 0) {
if (mouseX > width/2 - 100 && mouseX < width/2 + 100 && mouseY > height/2 + 40
&& mouseY < height/2 + 100) {
gameState = 1; // Change state to Gameplay
}
}
}
void keyPressed() {
if (gameState == 1) { // Only track movement keys during playing state, to be worked
on further using our boolean logic tomorrow
if (key == 'a' || key == 'A') p1Left = true;
if (key == 'd' || key == 'D') p1Right = true;
if (key == 'w' || key == 'W') p1Jump = true;
if (key == CODED) {
if (keyCode == LEFT) p2Left = true;
if (keyCode == RIGHT) p2Right = true;
if (keyCode == UP) p2Jump = true;
}
}
}
(Same as yesterday, worked with Aayush on his computer for main menu and timer)
a) The concept I worked on today was mostly dedicated to my partner Aayush, as
we were trying to implement a countdown timer in our game, specifically a 30
second one. We debated on whether we should use frameCount or millis, and
Mrs. Kim told us that using frameCount would be an easier pick for us and
simpler overall, and therefore, we stuck to frameCount and determined the logic
that we had to use for it. We also worked on the main menu (ending screen),
designing the overall display for what the ending screen would look like.
b) We did not fully implement the timer into the code today, since I have the main
code with images on my computer and Aayush is coding different methods on
the side, so we did not test the timer with our full code yet, but we got the timer
running, and soon we can ensure that it goes from 30 seconds to one second
overall. The main menu for the ending screen is also created, and we will be
implementing that really soon, specifically tomorrow, which is gonna be a really
important day for us because we will be combining a lot of logic and also trying to
run it perfectly.
c) The challenges we encountered was the debate between either using millis or
frameCount. I told Aayush that we should much rather use millis because it is an
inbuilt Processing function and it may be much easier to utilise it than using
frameCount and finding the entire logic behind it. This issue was solved after we
asked Mrs. Kim about it and she let us know that frameCount might be the easier
option if we want to build a timer for our game, so we went on with frameCount
and created a timer using it.
Day 4
Final Code Submission:
// Images
PImage playerR, playerP, playerBg;
// Game State Control
int gameState = 0; // 0 = Main Menu, 1 = Playing, 2 = Game Over
// Player Properties
float playerSize = 35;
float runSpeed = 5;
float jumpForce = -10;
float gravity = 0.4;
// Player 1 (Red) State
float p1X, p1Y;
float p1Vy = 0;
boolean p1OnGround = false;
// Player 2 (Pink) State
float p2X, p2Y;
float p2Vy = 0;
boolean p2OnGround = false;
// Game Scoring & Timer Control
boolean isP1It = true;
int p1Score = 0;
int p2Score = 0;
int totalTime = 30;
int timeRemaining;
int startFrame; // Tracks the starting frame of the round
// Safe Tag Cooldown System
int lastTagMillis = 0;
int tagCooldown = 1000; // 1 second of immunity before another tag can happen
// Input Trackers
boolean p1Left, p1Right, p1Jump;
boolean p2Left, p2Right, p2Jump;
// ONE BIG PLATFORM LAYOUT (Center X, Center Y, Width)
float[] platX = { 150, 350, 550, 750, 900, 250, 500, 750, 120, 380, 620, 880, 250, 500,
750, 150, 850 };
180, 110, 120 };
180, 120, 120 };
float platformHeight = 16;
float landingThresholdY = 8;
float[] platY = { 450, 460, 440, 470, 430, 370, 380, 360, 280, 290, 270, 300, 190, 200,
float[] platW = { 140, 120, 150, 110, 130, 160, 200, 150, 130, 140, 160, 120, 180, 150,
void setup() {
size(1000, 562);
pixelDensity(1);
playerR = loadImage("PlayerR.png");
playerP = loadImage("PlayerP.png");
playerBg = loadImage("TagGameBackground.jpg");
}
void draw() {
if (gameState == 0) {
drawMainMenu();
} else if (gameState == 1) {
drawGameplay();
} else if (gameState == 2) {
drawGameOverScreen();
}
}
// Main Menu Screen
void drawMainMenu() {
background(255, 235, 100); // Bright Yellow Background
textAlign(CENTER, CENTER);
fill(0);
textSize(50);
text("2D PLATFORM TAG", width/2, height/2 - 100);
textSize(20);
fill(50);
text("P1: W, A, D | P2: Arrow Keys", width/2, height/2 - 30);
// Draw Clickable Play Button
rectMode(CENTER);
stroke(0);
strokeWeight(3);
if (mouseX > width/2 - 100 && mouseX < width/2 + 100 && mouseY > height/2 + 40 &&
mouseY < height/2 + 100) {
fill(255, 255, 255); // Highlight white on hover
} else {
fill(240, 210, 50); // Darker yellow normally
}
rect(width/2, height/2 + 70, 200, 60, 10);
// Play Button Text
noStroke();
fill(0);
textSize(24);
text("PLAY", width/2, height/2 + 70);
}
// Gameplay Loop
void drawGameplay() {
background(playerBg);
// Outer Solid Boundary Wall Borders
fill(0);
noStroke();
rectMode(CORNER);
rect(0, 0, width, 45); // Top UI panel bar
rect(0, 515, width, 50); // Bottom solid boundary limit
rectMode(CENTER);
// Draw Solid Platforms
fill(74, 46, 26);
for (int i = 0; i < platX.length; i++) {
rect(platX[i], platY[i], platW[i], platformHeight, 4);
}
// Round Timer Controller via custom timer function
timer();
// Physics
processPlayer1();
processPlayer2();
checkTagContacts();
//nPlayer 1
image(playerR, p1X - playerSize/2, p1Y - playerSize/2, playerSize, playerSize);
// Player 2
image(playerP, p2X - playerSize/2, p2Y - playerSize/2, playerSize, playerSize);
drawChaserIndicator();
displayHUD();
}
// Custom Frame Count Timer
void timer() {
int seconds = 30 - ((frameCount - startFrame) / 60);
if (seconds >= 0) {
timeRemaining = seconds; // Update time remaining for game state tracking
} else {
timeRemaining = 0;
gameState = 2; // Move to Game Over screen
if (isP1It) p2Score++; else p1Score++;
}
}
// Game Over Screen
void drawGameOverScreen() {
background(255, 235, 100);
textAlign(CENTER, CENTER);
fill(0);
textSize(46);
text("ROUND COMPLETE", width/2, height/2 - 100);
textSize(28);
if (isP1It) {
fill(255, 120, 180);
text("PLAYER 2 (PINK) WINS!", width/2, height/2 - 20);
} else {
fill(255, 100, 100);
text("PLAYER 1 (RED) WINS!", width/2, height/2 - 20);
}
// Display Current Lifetime Scores
fill(0);
textSize(20);
text("Scores -> P1: " + p1Score + " | P2: " + p2Score, width/2, height/2 + 40);
textSize(16);
text("Press SPACEBAR to load next match round", width/2, height/2 + 110);
text("Press M to return to Main Menu", width/2, height/2 + 140);
}
// Movement and Ground Detection
void processPlayer1() {
if (p1Left && p1X > playerSize/2) p1X -= runSpeed;
if (p1Right && p1X < width - playerSize/2) p1X += runSpeed;
if (p1Jump && p1OnGround) {
p1Vy = jumpForce;
p1OnGround = false;
}
p1Vy += gravity;
p1Y += p1Vy;
//Platform Detection Logic (Player 1)
p1OnGround = false;
for (int i = 0; i < platX.length; i++) {
float platLeftEdge = platX[i] - platW[i]/2;
float platRightEdge = platX[i] + platW[i]/2;
float platTopEdge = platY[i] - platformHeight/2;
// Check if player's X coordinate is sitting within the platform width bounds
if (p1X > platLeftEdge && p1X < platRightEdge) {
// Find where player's feet touch down
float playerFeetY = p1Y + playerSize/2;
// If falling down, feet cross the platform top, but haven't fallen all the way past it
if (p1Vy >= 0 && playerFeetY >= platTopEdge && playerFeetY <= platTopEdge +
landingThresholdY) {
p1Y = platTopEdge - playerSize/2; // Snap perfectly on top
p1Vy = 0; // Stop falling speed
p1OnGround = true; // Authorizing jumps
}
}
}
}
if (p1Y > 515 - playerSize/2) { p1Y = 515 - playerSize/2; p1Vy = 0; p1OnGround = true; }
if (p1Y < 45 + playerSize/2) { p1Y = 45 + playerSize/2; p1Vy = 0; }
void processPlayer2() {
if (p2Left && p2X > playerSize/2) p2X -= runSpeed;
if (p2Right && p2X < width - playerSize/2) p2X += runSpeed;
if (p2Jump && p2OnGround) { p2Vy = jumpForce; p2OnGround = false; }
p2Vy += gravity;
p2Y += p2Vy;
// Platform Detection Logic (Player 2)
p2OnGround = false;
for (int i = 0; i < platX.length; i++) {
float platLeftEdge = platX[i] - platW[i]/2;
float platRightEdge = platX[i] + platW[i]/2;
float platTopEdge = platY[i] - platformHeight/2;
// Check if player's X coordinate is sitting within the platform width bounds
if (p2X > platLeftEdge && p2X < platRightEdge) {
// Find where player's feet touch down
float playerFeetY = p2Y + playerSize/2;
// If falling down, feet cross the platform top, but haven't fallen all the way past it
if (p2Vy >= 0 && playerFeetY >= platTopEdge && playerFeetY <= platTopEdge +
landingThresholdY) {
p2Y = platTopEdge - playerSize/2;
p2Vy = 0; // Stop falling speed
p2OnGround = true; // Authorizing jumps
}
}
}
if (p2Y > 515 - playerSize/2) {
p2Y = 515 - playerSize/2;
p2Vy = 0; p2OnGround = true;
}
if (p2Y < 45 + playerSize/2) {
p2Y = 45 + playerSize/2;
p2Vy = 0; }
}
// Cooldown and Collision System
void checkTagContacts() {
// If 1 second hasn't passed since the last tag, ignore all collisions
if (millis() - lastTagMillis < tagCooldown) return;
if (dist(p1X, p1Y, p2X, p2Y) < playerSize) {
isP1It = !isP1It; // Swap roles
lastTagMillis = millis(); // Start the 1 second immunity timer
}
}
void resetGame() {
p1X = 150; p1Y = 480; p1Vy = 0;
p2X = 850; p2Y = 480; p2Vy = 0;
isP1It = random(1) > 0.5;
startFrame = frameCount;
lastTagMillis = 0;
}
// Arrow on who is the IT
void drawChaserIndicator() {
float arrowX = isP1It ? p1X : p2X;
float arrowY = isP1It ? p1Y : p2Y;
stroke(0);
strokeWeight(1.5);
triangle(arrowX, arrowY - playerSize/2 - 6, arrowX - 8, arrowY - playerSize/2 - 22,
arrowX + 8, arrowY - playerSize/2 - 22);
noStroke();
}
void displayHUD() {
textAlign(CENTER, CENTER);
textSize(26);
fill(255);
text("" + timeRemaining, width / 2, 22);
textSize(16);
fill(255, 100, 100);
text("P1 (Red): " + p1Score, 150, 22);
fill(255, 120, 180);
text("P2 (Pink): " + p2Score, 850, 22);
}
// --- MOUSE CLICK DETECTION SYSTEM ---
void mousePressed() {
if (gameState == 0) {
if (mouseX > width/2 - 100 && mouseX < width/2 + 100 && mouseY > height/2 + 40
&& mouseY < height/2 + 100) {
resetGame();
gameState = 1;
}
}
}
// Key Inputs
void keyPressed() {
if (gameState == 1) {
if (key == 'a' || key == 'A') p1Left = true;
if (key == 'd' || key == 'D') p1Right = true;
if (key == 'w' || key == 'W') p1Jump = true;
if (key == CODED) {
if (keyCode == LEFT) p2Left = true;
if (keyCode == RIGHT) p2Right = true;
if (keyCode == UP) p2Jump = true;
}
}
if (gameState == 2) {
if (key == ' ') {
resetGame();
gameState = 1;
}
if (key == 'm' || key == 'M') {
gameState = 0;
}
}
}
void keyReleased() {
if (key == 'a' || key == 'A') p1Left = false;
if (key == 'd' || key == 'D') p1Right = false;
if (key == 'w' || key == 'W') p1Jump = false;
if (key == CODED) {
if (keyCode == LEFT) p2Left = false;
if (keyCode == RIGHT) p2Right = false;
if (keyCode == UP) p2Jump = false;
}
A and B ) Today was our final day and we had to combine everything together, and also
add things we planned earlier but did not get time to execute because of the days we
missed, it will be difficult to go through everything through text, so here are all the things
that are easily explained through text. First, I implemented arrays and data structures.
This was the most significant addition, as I mainly used it to generate all my platforms
properly so that the map looked visually appealing but not too perfect so that it was
harder to play on. I used three float arrays, platX, platY, and playW, each of who’s i
value will all dictate all the platforms, and the height for all will stay the same since we
want the platform size to stay the same. These three arrays are accessed in three
places, first is drawGameplay, to draw every platform (which is run by a for loop, looping
through the arrayLength, and assigning the i value of each array to the corresponding
height, width, x and y value, and etc.), and the second is processplayer(1 or 2 since we
have both) to run collision detection against every platform. I also added a
landingThreshold, since I want to calculate that once the player goes a certain amount
of pixels inside the platform, it will snap back to the platform entirely, I am keeping this
as 8 or 10. We also added our platform detection logic, where before it begins it states
that p(½)OnGround = false, which makes sure that the player is in the air when this
method is run. We loop through all platforms, and assign variables for the left and right
edge. We ensure that the players X coordinate is between the left and right edge
somewhere, and not over, and then ensure that players y velocity is >= 0, which makes
sure the player is falling (to account for going too far into pixel) or 0, which is on the
ground, we ensure that the players feet (bottom) is above the platform, and that the feet
haven’t fallen too far past the collision threshold, when all of these together are true, we
snap the player to the platform that they are on, and this is one of the best
implementations we have done in this entire project so far. We also implemented
cooldown and collision systems, where we implemented our 1 second cooldown, and
found distance between p1 and p2 and based on that implemented our collision system.
c) Our biggest challenge today was the time crunch. We had to implement a lot of things
that we had planned for, and mostly had the logic down for. We just had to write it down
and hope that our logic that we planned was perfectly fine to encounter no bugs. But
obviously, nothing is perfect, so we did encounter some bugs, we managed to fix some
bugs, and did not manage to fix others, but the ones we did not manage to fix were
essentially removed by changing methods up and removing some external features that
served no purpose whatsoever. Overall, we have 95% finished our entire project, and
we are happy with what we have accomplished, because we were already at a
disadvantage due to our extracurricular activities and having to leave school so often,
but we managed our time well, planned everything out well, and in the end finished the
project.
Day 5
I did not get an extra day since my partner Aayush used one of my days that was
provided since I was not here.
---
*Update this page by editing `index.md` in your repository.*
