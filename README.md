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