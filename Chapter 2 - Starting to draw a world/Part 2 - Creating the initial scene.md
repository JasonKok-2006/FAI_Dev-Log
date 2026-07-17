## 2.2 – Starting to draw a world - Creating the initial scene

With a basic initial spritesheet drawn, I can open Godot and start to build a world in which the player would be able to interact with (once we add the player character). However, I need a way to convert the spritesheet .png file into a world within the Godot scene.

![FAI hub first tileset](/Screenshots/Chapter2/2.2/fai_hub.png)

This is where a TileMap node comes into play. TileMapLayer node to be exact due to the TileMap node now being deprecated in Godot version 4.6.3. A TileMapLayer is just one layer of a TileMap, a tool which provides a grid system that can be filled with sprites to create static worlds quickly. Alongside the grid system, it allows me to create and manage tilesets which can be formed by slicing .png files, providing the solution of turning a spritesheet into a world. 

By using two layers (initially), one for the ground and one for the walls, it would make it easy to differentiate between a wall tile and a floor tile within FAI’s code. This would make different collision rules, or any other logical difference, simple to program when the time comes compared to only using one layer.

With the first room and used tileset being just a prototype design, I am happy for now about how the room turned out. Within the Godot engine, press F5 and … 

![First shot at the first room](/Screenshots/Chapter2/2.2/first_shot.png)

The room is a bit small compared to the game window.
