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
    3. [Zooming in](#)

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

![FAI hub first tileset](/Screenshots/2.2/fai_hub.png)

This is where a TileMap node comes into play. TileMapLayer node to be exact due to the TileMap node now being deprecated in Godot version 4.6.3. A TileMapLayer is just one layer of a TileMap, a tool which provides a grid system that can be filled with sprites to create static worlds quickly. Alongside the grid system, it allows me to create and manage tilesets which can be formed by slicing .png files, providing the solution of turning a spritesheet into a world. 

By using two layers (initially), one for the ground and one for the walls, it would make it easy to differentiate between a wall tile and a floor tile within FAI’s code. This would make different collision rules, or any other logical difference, simple to program when the time comes compared to only using one layer.

With the first room and used tileset being just a prototype design, I am happy for now about how the room turned out. Within the Godot engine, press F5 and … 

![First shot at the first room](/Screenshots/2.2/first_shot.png)

The room is a bit small compared to the game window.

## Part 3: Zooming in

As mentioned in the previous FAI Dev-log (2.2 – Starting to draw a world - Creating the initial scene), when I pressed F5, the room was tiny compared to the game screen. This could be fixed by just making the room larger, but this means larger sprites would be required for the characters to make the game enjoyable for the player. I mean as a gamer myself, I wouldn’t want to be squinting at the screen to see what is going on. 

So to fix the tiny room situation, we need a way to zoom into the scene. This is where the Camera2D node comes in. By adding this node, the game screen now snaps to the scope inside the camera box rather than the default scope that the scene normally has. As this scope is customisable, I am able to customise the scope that the camera sees by changing parameters such as position and scale. By increasing the scale, the scene zooms in and the problem is fixed. 

![Attempt 2](/Screenshots/2.3/take2.png)

However, something still seems off about the room. 
