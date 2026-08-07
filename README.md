# FAI_Dev-Log
FAI is a game I plan to make as a summer project enhancing my fluency in C# and technical fundamentals. While FAI's repository is set to private, this repository will show the steps, design choices and code snippets that are involved within FAI's development process. 

Ever since I started learning to code, I knew I enjoyed solving problems using software. It will be a genuine pleasure to do this for a living. Therefore, I have tried to make the dev-logs informative whilst being readable in hopes that a recruiter takes the time to read this. 

---

# Chapters
1. **Pre-development discussion**
    1. [Project defined](#part-1-project-defined)
    2. [Git repo initialised](#part-2-git-repo-initialised)
2. **Starting to draw a world**
    1. [Art direction](#part-1-art-direction)
    2. [Creating the initial scene](#part-2-creating-the-initial-scene)
    3. [Zooming in](#part-3-zooming-in)
    4. [What seemed off, now seems on](#part-4-what-seemed-off-now-seems-on)
3. **Giving the protagonist a acharacter**
    1. [Initial design](#part-1-initial-design)
    2. [Adding a player scene](#part-2-adding-a-player-scene)
    3. [Nothing to show](#part-3-nothing-to-show)
    4. [Visualising energy](#part-4-visualising-energy)
	5. [Expanding the energy system](#part-5-expanding-the-energy-system)
	6. [Finishing touches for now](#part-6-finishing-touches-for-now)
4. **Determinising randomness**
	1. [Outlining the PRNG](#part-1-outlining-the-prng)
	2. [Optimised implemetation](#part-2-optimised-implementation)
	3. [Putting it to use](#part-3-putting-it-to-use)
5. **Meet FAI**
	1. [Trigger warning](#part-1-trigger-warning)
	2. [On screen](#part-2-on-screen)
	3. [Awaiting typewriter text](#part-3-awaiting-typewriter-text)

---

# Chapter 1: Pre-development discussion
## Part 1: Project defined

The usage of AI has increased recently throughout the industry. As more coding tasks become automated, it is becoming clear that development jobs now become a task of testing and optimising AI outputs, rather than starting from scratch, as it was traditionally done. With code review and optimisations becoming a bigger part of the job, it’s more important than ever to understand the fundamentals of what makes good quality code compared to a poor quality code which looks like it works (until it breaks). That is why I plan to make a game (FAI), without the help of any AI tools.

To achieve this, I have defaulted to using Godot. While I have experience using Unity, Unity’s new AI assistance features will defeat the whole purpose of the project. To make a game without AI, protesting the overuse of AI within the industry (as it creates an unknown technical debt).

I get that AI tools are tools which are readily available to people and can often be used in a beneficial way (and I support that). However, with entry level positions declining and AI being used as an excuse for mass layoffs, it makes sense for me to theme a game over the disruption AI has caused so far. 

I have decided to use the .NET version of Godot, using C# as the language in which FAI will be programmed in. While GDScript is supposedly easier to develop in, my experience with Unity means I will be able to handle the use of C# which will make it easier to switch back to Unity in the future. 

## Part 2: Git repo initialised

For a major software project, such as a game, the future should always be accounted for as much as possible. Therefore, we need to be prepared when something decides to break. This is where Git repositories come into play. Git repositories allow us to prepare for such events, such that when the code breaks, a previous stable version can at least be restored. Git repositories also allow us to branch out and try new features before fully committing to them. If the feature ends up not working or being fun, then we just delete the branch and revert back to the main branch built so far. 

Git repositories can also be published on a hosting platform to ensure that a backup exists. This accounts for any hardware failures that I may run into in the future. If my laptop breaks, then I will be able to access the current state of the project easily on a new device. This also allows me to share the current state of the project with other people in case people want to take part in the project. The hosting platform of my choice is GitHub. 

GitHub provides GitHub Desktop, which is a GUI application designed for beginners to make publishing the Git repositories to GitHub easier and more intuitive. **This application will not be used in the development of FAI**. Instead, I will be using the traditional CLI application mainly due to my experience with the traditional CLI application. Another, reason is that GitHub Desktop being more constrained than the traditional CLI application allowing for better management of the project.

# Chapter 2: Starting to draw a world
## Part 1: Art direction

I’ll admit, I’ve never been great at art, as I come from a technical background. So at the moment when it’s just me developing FAI and I want to create a world from scratch, there is only one option available for an artstyle to create my sprites in. Pixel art. 

By creating my tilesets with pixel art, I can accurately draw details I am happy with into my sprites in a timely manner. This allows me to showcase the journey leaning into a more technical side, compared to a more creative side. While both sides are important for a game developer’s skill set, I’m developing this game to advance my understanding of technical fundamentals further. Hence, spending too much time on the art for this game seems counterproductive. 

To draw scenes efficiently, I have settled on using a 16x16 pixel tile size rather than 32x32. With smaller tile sizes, less art is repeated. By splitting up the tiles into smaller squares, complex patterns can be made up by piecing multiple smaller tiles together. These small tiles can be swapped out for alternative tiles allowing for an easy manipulation of the patterns without having to redraw previously made art.

## Part 2: Creating the initial scene

With a basic initial spritesheet drawn, I can open Godot and start to build a world in which the player would be able to interact with (once we add the player character). However, I need a way to convert the spritesheet .png file into a world within the Godot scene.

![FAI hub first tileset](/Screenshots/Chapter2/2.2/fai_hub.png)

This is where a TileMap node comes into play. TileMapLayer node to be exact due to the TileMap node now being deprecated in Godot version 4.6.3. A TileMapLayer is just one layer of a TileMap, a tool which provides a grid system that can be filled with sprites to create static worlds quickly. Alongside the grid system, it allows me to create and manage tilesets which can be formed by slicing .png files, providing the solution of turning a spritesheet into a world. 

By using two layers (initially), one for the ground and one for the walls, it would make it easy to differentiate between a wall tile and a floor tile within FAI’s code. This would make different collision rules, or any other logical difference, simple to program when the time comes compared to only using one layer.

With the first room and used tileset being just a prototype design, I am happy for now about how the room turned out. Within the Godot engine, press F5 and … 

![First shot at the first room](/Screenshots/Chapter2/2.2/first_shot.png)

The room is a bit small compared to the game window.

## Part 3: Zooming in

As mentioned in the previous FAI Dev-log (2.2 – Starting to draw a world - Creating the initial scene), when I pressed F5, the room was tiny compared to the game screen. This could be fixed by just making the room larger, but this means larger sprites would be required for the characters to make the game enjoyable for the player. I mean as a gamer myself, I wouldn’t want to be squinting at the screen to see what is going on. 

So to fix the tiny room situation, we need a way to zoom into the scene. This is where the Camera2D node comes in. By adding this node, the game screen now snaps to the scope inside the camera box rather than the default scope that the scene normally has. As this scope is customisable, I am able to customise the scope that the camera sees by changing parameters such as position and scale. By increasing the scale, the scene zooms in and the problem is fixed. 

![Attempt 2](/Screenshots/Chapter2/2.3/take2.png)

However, something still seems off about the room. 

## Part 4: What seemed off, now seems on

As mentioned in the previous FAI dev-log (2.3 – Starting to draw a world - Zooming in), something seemed off about the initial room. 

![Attempt 2](/Screenshots/Chapter2/2.3/take2.png)

So I went to my inspiration for this project, Stardew Valley. I booted up my Nintendo Switch and loaded up my file I reached perfection on and started playing. Walking around the house, I realised an obvious thing. To create this perspective of top down (but not fully birdseye), the bottom wall has to cover the floor slightly. This fix needed some new tiles which I had to draw.

Walking around the house in Stardew Valley a little more, I noticed slight shadows along the walls. While they were not massively noticeable at first, they help distinguish the walls from the floor in a natural way. So let’s add them! To do this, again new sprites would be created to represent the shadows. Adding a new TileMapLayer node for the shadow sprites I positioned the shadow layer so Godot displays the ‘Ground’ layer first, ‘Shadow’ layer second and the ‘Wall’ layer last. However, this led to a slight problem, LibreSprite (the application I used to create the sprites) uses RGB (Red, Green, Blue) values. This means no degree of transparency was offered, leading to the shadows being a solid black sprite. 
 
The fix for this is making use of Godot, as it offers a variety of options to customise the node, including RGBA (Red, Green, Blue, Alpha) values. This is found in the node’s Inspector > Visibility > Modulate. RGBA adds the ‘Alpha’ parameter, which decides the opacity of the object (0 for fully transparent - 255 for fully visible). By adjusting the RGBA values of a TileMapLayer, the sprites can become darker than the original import, be given a coloured tint, and also become more transparent. The default RGBA values are (255, 255, 255, 255) which provides a white lighting (default sprite) and fully opaque. By reducing the ‘Alpha’ value, a solid black edge can be turned into a translucent shadow. 

With the aim to make the room have a dystopian feel, the flooring felt too light. Hence by lowering the ‘Red’, ‘Green’ and ‘Blue’ values on the RGBA value for the ‘Ground’ TileMapLayer, the floor becomes darker, saving me from redrawing the ground sprites. 

![Attempt 3](/Screenshots/Chapter2/2.4/finished.png)

With all that, we now have an empty room which is ready to go. Now what’s missing is a character which the player can control. 

# Chapter 3: Giving the protagonist a character
## Part 1: Initial design

As already established in FAI Dev-log 2.1 (Starting to draw a world - Art direction), pixel art allows for quick designs for the spritemaps used for FAI. However, while the 16x16 pixel tile size works for tilesets related to the world, I chose to give a tileset size of 32x32 for the protagonist. Then by splitting the character into 3 sections (head, body, thruster), I can group each part together to form the protagonist. This saves having to draw every combination and also splits the logic for the correct animations which simplifies the program’s logic, which allows me to easily edit the file if I have to in the future.

The reason why 32x32 pixel size was used for the protagonist was solely due to the head portion of the character. If I used 16x16 pixel size for the character, the facial expressions become rather limited due to the space that would be given to the eyes and mouth (4x2 compared to the 8x4 that a 32x32 pixel size allows). As I also previously mentioned in FAI Dev-log 2.1 (Starting to draw a world - Art direction), I am a novice artist. Hence, the character is a limbless robot making it easier to draw and animate for me as I improve my artistic capabilities. This means to stop the protagonist feeling lifeless, the only option is to majorly enhance the facial expressions giving the protagonist personality. 

All in all, putting the character together, I'm pretty happy how it looks once its in the Godot scene.

![The initial design of the character](/Screenshots/Chapter3/3.1/Initial.png)

## Part 2: Adding a player scene

Now we have a spritesheet for our player character, it's time to add the character into our scene. So I searched for a tutorial on how to do this in Godot for the engine syntax and of course every tutorial uses GDScript. Great. This means for most tutorials in Godot, for me to follow, I need to translate the logic from GDScript to C#. While this slows down development slightly, this forces me to understand the logic within the tutorial before it gets implemented into FAI. Understanding GDScript is surprisingly intuitive as it reminds me a lot about Python with some Haskell syntax. Skim through the video and … we can import scenes into other scenes! 

While this doesn’t sound like a massive deal, it allows development of the game to be done through multiple scenes (e.g. a world scene, a player scene, a map scene) which can all be combined into a new main scene which is the full game. This makes the game easier to alter as if the world needs to be changed, then there is no risk in accidentally modifying the characters. 

To add a character in Godot, I found using the AnimatedSprite2D solves this problem. This node is capable of holding many animations regarding the sprite we want to show. By adding an AnimatedSprite2D for the head, body and thruster parts of the character, they can all be grouped by making them all children of a CharacterBody2D node. Adding a basic character movement script to the CharacterBody2D node, we now have the first C# script and a controllable character! Press F5 and the animations work as intended; the code works. After the initial excitement of the progress, I came to the realisation … FAI isn’t anywhere near being fun. But I guess that is to be expected as the project is just starting out. 

![Recording 1](/Recordings/3.2/recording1.mp4)

P.S. The gameplay recordings sit in the FAI project folder, as it makes it easier to find for later uses such as showing progress through comparisons. These recordings make no sense to include within the GitHub repository as they aren’t necessary to the project. This is where .gitignore comes in. Any file or subdirectory which we don’t want shared, whether it’s unnecessary or for security reasons (e.g. API key files), .gitignore will ensure the files won’t be pushed to github.

**.gitignore is not used for the screenshots and video recordings for this repository. Why? Because these files need to be shared in the repository for the media to be displayed.**

## Part 3: Nothing to show

For a videogame to be enjoyable, there has to be some way to ‘lose’ within the game. The most common method of implementing a way to lose within the game is to implement a version of a health system. Even Animal Crossing New Horizons, known for being a cosy life sim game, implements losses through fainting when being attacked by a tarantula, a scorpion or if you’re stung by wasps twice. Within Animal Crossing New Horizons, medicine can be bought at Nook’s Cranny to counteract the wasp’s sting giving the player a chance to heal. 

As mentioned in FAI Dev-log 3.1 (Giving the protagonist a character - Art direction), the protagonist is a robot due to artistic constraints. So let’s lean into this. Taking inspiration from Chibi-Robo!, a Nintendo Gamecube adventure game where you play as a miniature robotic assistant doing household chores, Chibi-Robo! uses energy as a health system. The player constantly has to monitor the battery usage throughout the gameplay, and has to find power outlets scattered around the house to recharge. FAI, as the protagonist is a robot as well, will similarly include a health system as energy. This means the player loses when the character reaches zero charge. The player will lose charge over time naturally in hopes to make the game feel intensive, turning the simulation game into a ‘time-attack’. Enemies and obstacles will also be implemented which will also decrease the energy level the player has. By using one health system for gradual decline and being hit by opposing hitboxes, the player is forced to find balance with being careful navigating the world and making sure they move quickly. While the script has been programmed, there are no enemies or any UI element showing the energy level of the player, meaning as of yet there is nothing to show.

However, with nothing new to show, I want to take the time to emphasise human oversight on coding. You can have a script which can behave in a desired way but there is a difference between spaghetti code and clean code. Clean code ensures stability within the codebase as variables get accessed and altered through getters and setters. Constants for magic numbers and consistent naming conventions allows for the code to become more readable. Splitting up larger functions into smaller functions and larger scripts into separate scripts (one for the health system, one for the movement, etc) allows the code to be maintainable by making it easy to find the exact piece of code which is currently failing. Having human oversight on this ensures the codebase remains clean, even if the scripts are being AI generated (which is not the case for FAI). All these benefits found in clean code, emphasise the point on why human input is still majorly important within the world of software engineering during this AI era, further signifying the importance of being knowledgeable on technical fundamentals. 

## Part 4: Visualising energy

The last FAI dev-log (3.3 – Giving the protagonist a character - Nothing to show) mentioned that there was no visual representation of the health system. So before we move on to the next thing to implement, let’s finish the energy system. To do this, we need a CanvasLayer option in the main game scene. A canvas layer size snaps to the game screen size, allowing any Control (UI) nodes to be repositioned and rescaled to what the current game screen is. This ensures consistent UI layouts between different devices that have different screen resolutions. 

The energy bar is made by using a TextureProgressBar. This node provides fields for ‘Under’ (the background sprite), ‘Over’ (the foreground sprite) and ‘Progress’ (the sprite between which the percentage shown is based on the node’s value) textures. For the energy bar, a battery outline is used for the ‘Under’ sprite and a basic white shape fill is used for the ‘Progress’ sprite. The ‘Over’ sprite is left at null. 

Now we have a representation of energy added to the main game scene, we need a way to display the correct values. First problem, the character is in its own scene, therefore we need to ensure that the main scene has access to the player scene’s values. What seemed like a hard task initially, was made trivial after some research. By ensuring the root node of the player scene has the script controlling the scene (the player in this case), we can attach the same script to the imported player scene in the main scene. This means any variables we need can now be accessed between scenes.  

Now that we have access to the player script from another scene, we have something to think about. The game state updates every frame. However, the current energy system at the moment decrements the energy every 0.5 seconds. With the target frame rate at 60 frames per second, it means for every second 2 out of 60 frames have an energy level change. So if we update energy levels in _PhysicsProcess, such that the health bar gets updated every frame, we have 58 frames per second of unnecessary updates. This can be solved by creating a custom signal and updating the health bar once the custom signal has been emitted. Signals allow for data to be transferred between scenes without the other scene having to look within the other scene’s script, as the emitter can send out temporary values any receiver can read from. By using signals, we update the health bar visual only when there is a health change, eliminating 58 unnecessary updates per second. 

```csharp
private const int GREEN_RANGE = 70;
private const int AMBER_RANGE = 30;
private const int BLUE_VAL = 40;
private const int ALPHA_VAL = 255;
private const int MAX_RGBA_VALUE = 255;

public void CalculateTint(int currentEnergy, int fullEnergy)
{
	int batteryPercentage = (currentEnergy * 100) / fullEnergy;
	int redVal;
	int greenVal; 

	if (batteryPercentage >= 30)
	{
		redVal = MAX_RGBA_VALUE - (((batteryPercentage - 30) * MAX_RGBA_VALUE) / GREEN_RANGE);
		greenVal = MAX_RGBA_VALUE;
	}
	else
	{
		redVal = MAX_RGBA_VALUE;
		greenVal = (batteryPercentage * MAX_RGBA_VALUE) / AMBER_RANGE;
	}

	EnergyBar.TintProgress = Color.Color8((byte)redVal, (byte)greenVal, BLUE_VAL, ALPHA_VAL);
}
```

By using a solid white fill for the progress texture, RGBA tint values can be calculated based on the battery percentage that the player currently has. This allows for smooth colour change as the player’s energy depletes adding a sensible additional visual cue to the player, warning them that their time is running out.

![Energy bar visual recorded](/Recordings/3.4/recording2.mp4)

I want to finish this dev-log by talking about this line of code:

```cs
int batteryPercentage = (currentEnergy * 100) / fullEnergy;
```

The intuitive way to calculate batteryPercentage is:

(currentEnergy / fullEnergy) * 100, 

However, a slight problem, ints are used to represent the value of energy meaning the code is bound to integer arithmetic. This means decimals can’t be processed. So suppose we substitute values into the following values into this formula:

(60 / 120) * 100,

We get the answer 0, when we expect 50. This is because when using integers, the decimal becomes truncated, which means the equation becomes:

(60 / 120) * 100
= (0) * 100  
= 0

Which is a hard to find culprit for health related bugs. I came to the realisation that order of operations matter by printing the values using GD.Print() which is Godot’s version of Console.WriteLine(). Therefore the arithmetic bug has been fixed by rearranging the formula. While I am aware floats could have been used instead, making this debugging process irrelevant, computers have a hard time evaluating exact values for floating point calculations. Famously, 0.1 + 0.2 = 0.30000000000000004. With this game being treated as a time attack, too many floating point calculations leads to inconsistencies, which could create slight time differences potentially big enough to cause inconsistencies within the time limit. 

## Part 5: Expanding the energy system

Splatoon, in my opinion, is one of the best designed game franchises ever made. Nintendo took the team vs team shooter genre, popularised by graphic series such as Counter-Strike and Call of Duty, and designed a family friendly entry to the genre. This was done by turning realistic weapons into ink-charged weapons, creating a paintball theme to the game. Leaning into the family friendly design, games aren’t conditioned solely on kill count, rather 5 different modes which focus on territory control. These match conditions often allow for less experienced players to still remain competitive against experienced players within the shooter genre, as the game doesn’t explicitly reward kills. That goes without saying; of course killing will help your team win the match. 

With the weapons being ink-charged, the characters you play as are inklings. Inklings are human characters that can morph into squid form. Players can shoot in human form, whilst moving stealthier and accessing more areas in squid form. The switch between these two forms create depth and strategy to what would otherwise be a simple shooter. Ammunition is switched for ink stored in an ink tank, which squid form will recharge quickly if you swim in your own colour ink. Players have to keep track of their ink meter, otherwise your weapons don’t work and you’re left useless. This is also translated well for Inkling’s design in Super Smash Bros Ultimate, where certain attacks are less effective (or straight up don’t work) if you run out of ink. 

So why have I spent the opening 2 paragraphs praising Inkling’s design rather than talking about my development process? Well, taking inspiration from Super Smash Bros Ultimate, FAI’s energy system will limit the character’s option in “low battery” mode, cutting off processes entirely. This feature will become clearer in the future when actions such as combat will be implemented but for now let's implement a “battery saver” with movement. 
To do this we create a new action, such that when the player presses shift, the player speeds up. Once the player reaches “low battery” (15% of the maximum energy), we aim to cut the player off from moving faster. To help translate this into the script, Godot offers _UnhandledInput, a function that triggers when a key is pressed. Figuring out how to recognise the shift input, to say adding the “battery saver” went smoothly, I’d be lying. So let me paint the scene and describe the process. 

My first attempt handled speed through one variable and constant speed multiplier. We set the new speed in shift mode by multiplying the value by the speed boost, and dividing by the speed boost when we no longer shift. Initially, IsShifting (a variable storing a boolean on if we should be moving fast) was overridden to false no matter what in “battery saver” and speed was recalculated after each press by a ternary operator based on the condition of IsShifting. This means pressing shift in “battery saver” divides the speed to go smaller than intended. Repeatedly press shift and the speed reaches 0. Yeah … that’s not meant to happen. Fixing this, more than one variable is used to set the player speed, avoiding the dynamic calculation which causes the value corruption. 

After all that was figured out, the character didn’t automatically go into "battery saver” when it reached below 15% health. So, to do this another custom signal was added and triggers when the health reaches below 15%. This avoids the code repeatedly resetting the speed value as the condition allows for the code to trigger once compared to every frame if it was pushed within _PhysicsProcess(). 

## Part 6: Finishing touches for now

Looking at the game scene, something still seemed off. The character is meant to be floating in the air but there was no way to tell. This is because there is nothing to visualise where the player is. Many 2D games, including Stardew Valley, fix this problem by putting a shadow beneath the character’s feet to generate depth within the 2D plane. This was my original solution as well, however, one slight problem. My artistic direction swapped legs for a fire based thruster. 

While games don’t always have to make sense, like tell me why I can fit 40 sharks in my pockets in Animal Crossing New Horizons, some elements do for an immersive effect. Putting shadows directly beneath a flame (a light source), breaks physical immersion inside a videogame. With that thought, the shadow solution is no longer on. My next thought was a burn trail. This could leave a short trail behind the character, which also breaks immersion as materials don’t magically get rid of burn marks, and permanent burn marks will essentially hide the art which makes up the world. So taking inspiration from the shadow, I created a simple animation of a ring of fire, to highlight the exact position of the player in an immersive way.

!["Final verison of the character for now"](/Recordings/3.6/recording3.mp4)

Now we have something to mark the position of the player, we might as well ensure the player interacts with the world correctly before moving on. To do this, a CollisionShape2D node is needed, which will act as a hitbox limiting where the player is able to go. To create the hitboxes for the walls, a Physics Layer is created, allowing for each tile within the tile set to hold a custom hitbox, which interacts with the ring of fire.

The last thing needed to be done here is “y-sorting”. This dictates whether Godot should draw a sprite behind or in front of an object by comparing y-values with the sprite (default value is 0). A tutorial and some funny attempts (with the character fully disappearing) later, y-sorting has been solved, creating more immersion as the player scene is partially hidden behind the bottom wall. 

With all of that done, the initial design of the protagonist is finished. While it is mute, the only logical sound effect so far would be a flamethrower. This will not be implemented as a constant stream of a repetitive sound will become stale quickly. A sound system will be dealt with later.

The one final touch I want to add to the protagonist’s character is random intervals between the blinks. I could just use the random class Godot offers, but I have something special planned. 

# Chapter 4: Determinising randomness 
## Part 1: Outlining the PRNG

Randomness exists in games to keep a game fresh over many playthroughs. It’s a way to stop the player from strategising the whole game beforehand and forces them to adapt to the situation. Take a game like “Mike Tyson’s Punch-Out!!”, randomness within each fight forces the player to react to each attack rather than eventually memorising a set of inputs, preventing the 14 fights within the game from becoming stale. While randomness boosts enjoyability in the game for the average player, it can negatively impact the speedrunning scene when too many random elements will make or break a speedrun outside of the player's control. 

I myself am very fond of the speedrunning scene in videogames. Having achieved the world record time on some levels found in the “Popular” menu in “Super Mario Maker 2” along with speedrunning many games casually, I love the idea of the speedrunning community coming together to push a game to its limit. So when random elements dictate a time loss near the end of a run, it becomes very frustrating. That’s why within FAI, all supposedly random elements will be generated using a Pseudo-Random Number Generator (PRNG), which certain actions from the player will affect the outcome. This allows for speedrunners to map out certain routes within the game to push the game to its limit while keeping the game seemingly random for casual players.

So, we need a formula to do this. Taking inspiration from the Diffie-Hellman (DH) key exchange, a cryptographic method primarily used to exchange secret keys over a public network, seemingly random integers can be generated. The formula is as follows:

**y = g^x mod p (g to the power of x)**

By choosing a suitable value for both p and g, along with a value for x which is calculated through a mix of player controlled actions and general incrementations, a seemingly random integer between 1 and p-1 will be generated. By calculating the value of y this way, the player will be able to control elements in the game in a stable manner as the framework p and g values aren’t affected by the player. Instead, the p and g values will be selected based on the scenario. To turn the integer given into a float (if needed), the formula used will be:

**float = y / p**,

Which also signifies the importance of choosing a suitable value for p. This will generate a float between 0 and 1. 

An added benefit to this randomness system is predetermined values can allow for quick testing. Instead of waiting for the random event to happen, manipulating the values beforehand allows for the game to be tested with all outcomes quicker without having to implement an extensive cheat code system to manipulate the randomness. 

## Part 2: Optimised Implementation

Videogames have to run smoothly for them to be enjoyable. Often at times, great games such as “The Legend of Zelda: Breath of the Wild” have been criticised for frame drops in certain parts of the game such as “Korok Forest”. Even though the game is positively received in general, frame drops within games will always be negatively critiqued. 

Say a game has a target frame rate of 60fps (frames per second). Every maths, physics and visual update within the active scope has to be completed before the game can update to its next frame. This means everything that makes up the game has to be updated within ~0.016 seconds for the game to run smoothly. This highlights the definite need for optimisation within the project as slow algorithms can lead to a slower game. 

This is where time and space complexity come into play. Both complexities measure the efficiency of an algorithm, with time complexity affecting frame rate and space complexity affecting RAM usage. To simplify the complexity, big O notation tells us how much an algorithm’s efficiency declines with larger inputs. 

![Big-O graph](/Screenshots/Chapter4/Part2/1_5ZLci3SuR0zM_QlZOADv8Q.jpg)
*Credit to this website https://medium.com/swlh/basics-of-big-o-notation-7d5d905d058d*

In the last FAI Dev-log (4.1 – Determinising randomness - Outlining the PRNG), the PRNG was outlined into how it would work. Now as a basic coding exercise, implementing the intuitive way is not always the best way. A function like this is correct but it has an O(n) complexity. 

```csharp

// This is the version that is called in every other script
public static int GenerateNewRandomNumber(int p, int g, int x)
{
    return GenerateNewRandomNumber(p, g, x, 1); // Helper solely to elinate the addition of the 4th argument.
}


// Previous unoptimised verison
public static int GenerateNewRandomNumber(int p, int g, int remaining_x, int current_y)
{
    if (remaining_x <= 0) // reached the end of the exponential sequence
    {
        return current_y; // return the final result
    }

    int updated_y = (current_y * g) % p; // One step in the exponential process
    return GenerateNewRandomNumber(p, g, remaining_x - 1, updated_y); // recursively call decreasing a step
}

```

After a little research to look for optimisations, a fast calculation method (known as fast exponentiation) provides an O(log n) complexity. This means if the value for x (the exponential) is a 1000, we can calculate the result in ~10 calculations compared to ~1000 needed before. More extreme examples will provide a more significant time save when using this function, allowing the use of larger values as it won't affect the overall performance of the game.

```csharp

// This is the version that is called in every other script
public static int GenerateNewRandomNumberInt(int p, int g, int x)
{
	int currentTotal = 1;
	int previousIndex = 0;
	int previousValue = g;
	int moddedX = x % p;

	char[] binaryx = Convert.ToString(moddedX, 2).ToCharArray(); // take the binary of x
	Array.Reverse(binaryx); // reverse it

	for (int i = 0; i < binaryx.Length; i++)
	{
		if (binaryx[i] == '1')
		{
			int indexValue = FastModExponential2(p, previousValue, i, previousIndex); // Get the mod value for that specific power.
			previousValue = indexValue; // Update the previous value variable so the fast mod function works for the next iteration. 
			previousIndex = i;
			currentTotal = currentTotal*indexValue % p; // multiply the index againt the current total
		}
	}
	return currentTotal;
}

public static int FastModExponential2(int p, int y, int i, int lasti)
{
    if (lasti < i) // lasti is used as savepoint. This will optimise this function by reducing average tiem complexity of O(n) to O(1) (n being length of binary string)
    {
        int newy = y*y % p; // Calculate the value of the next largest power of 2
        return FastModExponential2(p, newy, i, lasti+1); // Recursively call if we dont have the correct exponential 
    }
    return y; // y holds the correct result
}

```

## Part 3: Putting it to use

Back in FAI Dev-log 3.6, I mentioned I wanted to make the character blink in random intervals. So, let's do that!

Slight problem though. The current custom API we made doesn’t support ranges. Ranges are required in this blinking scenario because when a human blinks naturally, very rarely they will have to blink again a second later, so we can eliminate small numbers like 1, 2 or 3. So we need a way to take the number we have from the range between 1 and p-1 into a custom range. Well, to do that, we can just use this function:

```csharp
// Variation for a range between the min and max
    public static int GenerateNewRandomNumberInt(int p, int g, int x, int min, int max)
    {
        int range = max - min;
        float result = GenerateNewRandomNumberFloat(p, g, x);
        return (int) MathF.Round(result * range) + min;
    }
```

Where we find the float result and multiply that by the range. Adding the minimum value in the range guarantees a value generated between the specified min and max arguments.

Before we use this API, testing has to occur. Enough testing has to be done to ensure that the formulas have been programmed successfully. This is where unit testing comes in. A script containing many test cases which when executed, compares the API results to the expected results. Once enough test cases have been made and they all pass, we can guarantee that the API works as expected (creating seemingly random values).

So back to the character’s blinking problem. This can be solved by choosing the min value 4 and the max value 9, where the intervals for blinking are seemingly random. The value of p is 67 and the value of g is 50 (no reason for these specific values). The value of x is determined from when the player starts the game, how many times the player has blinked so far. A variable keeps track, incrementing by 1 every time the player blinks, so a fresh result is called each time from the API. 

No player controlled actions can affect this interval. While I specifically designed the PRNG this way so the player can affect randomness, some niche random elements within the game really does not need a player input!

# Chapter 5: Meet FAI 
## Part 1: Trigger warning

Every game needs some objective for the player to work towards. In the case of Stardew Valley, it's initially rebuilding the community centre. In the case of Minecraft, an open world sandbox game, it’s defeating the Ender Dragon. 

In the case of FAI, it’s collecting data for **FAI (Fragmented Artificial Intelligence)**, directly taking inspiration from the work I was doing for DataAnnotation for over a year now. The data collection goals are going to work like Stardew Valley community centre and Animal Crossing series' museum, which takes a chore-like task and makes it fun and rewarding. 

Before we implement FAI, we need a way to activate him, some sort of trigger. Well FAI can’t be activated constantly, it’s a software which means we need some hardware to support it. A screen and well … the player character. 

To activate the screen, we need something to turn it on. Something obvious to which a player can tell they should activate. A pressure plate. 

This can easily be done with a new TileMapLayer node which displays the pressure plate and an Area2D node. Area2D nodes have built in signals which can be used to trigger functions when colliders enter and leave the defined area. By creating a script where the tileset gets swapped out when the player steps on the trigger and swaps back to the default when the player steps off the pressure plate, the problem of making an interactive pressure plate is solved.

Well with the trigger set up, visually warning the player about activating FAI, the next step is to implement the character.

![Showcase of the pressure plate](/Recordings/5.1/TriggerCreated.mp4)

## Part 2: On screen

So we have a screen for FAI and a button to activate it. Now, we have to get some response from FAI. To make a solid fill to turn the screen on, a rescaled 1x1 pixel is revealed when the player steps on the trigger. 

Considering FAI is a character based on LLMs, let's make a text generation animation, where extremely low poly text is displayed to FAIs screen to match the dialogue box planned for later. 

To do this, take the 1x1 white pixel sprite and modulate it to display a black version. Once one iteration of the sprite can be created and destroyed, loops can be used to display more iterations. Taking the position of FAI within the scene and taking the positions/lengths of FAI, the correct position of the sprite can be calculated. Keeping track of how far along the line the script is, if the sprite still fits on the line it gets placed and if not then the sprite goes onto a new line. 

Multiple sprites can be handled within a Queue. A First-In-First-Out data structure along with a custom struct which only contains a Sprite2D field (the word sprite) and an int field (the current row of the sprite). This allows a scrolling effect within the animation, as the Queue gets reset decrementing all previous sprites by 1 and the position gets recalculated based on the new row. If the new row is -1, then the sprite is never re-enqueued and gets deleted. 

Due to the sprite being created by the script, the automatic pivot point of the sprite is in the middle. This has to be kept in mind with the positioning of the sprite, where the sprite gets placed at the X position, half a sprite length away from the position we want to actually add it to. 

![FAI's sreen made](/Recordings/5.2/FAI%20Screen.mp4)

## Part 3: Awaiting typewriter text

So now we have an animation that plays when FAI is telling us something, it’s time to add a dialogue pop-up to the trigger. To do this, a function is attached to the trigger’s signals which plays the animation revealing the Panel and RichTextLabel nodes when needed. 

To make sure the dialogue fits within the scenes in the game, a custom pixelated font was created for this game. However, due to licensing issues within the software I used to create the font, I couldn’t use the font I created if it’s in a sold product. So for now (to save another afternoon’s worth of work), an open-sourced font package is being used. I hope to change this back to my custom font I made at some point in the future when redesigning the art but for now, I’m just going to use the open-source font and move on.

Playing Stardew Valley, the character’s dialogue reveals one letter at a time. This is known as the typewriter effect, which is a common work around games to eliminate throwing too much to the player at once. To reveal one letter at a time, we need to dynamically create a timer, which when finished a character is revealed and the next character is revealed. This can be easily done as RichTextLabels have a VisibleCharacters parameter which reveals the amount of characters specified. 

However, this is where the async and await keywords come into place. The async keyword marks the function such that when it is paused, the main thread does not get blocked. The await keyword pauses the execution of the function until the task has finished (in this case is the timer’s Timeout signal being activated). Together, this allows the typewriter effect to play smoothly. 

Create a dummy dialogue text, hit play and it works!

![Typewriter Text Showcase](/Recordings/5.3/Video%20Project%209.mp4)