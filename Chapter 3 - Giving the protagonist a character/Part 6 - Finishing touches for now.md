## 3.6 – Giving the protagonist a character - Finishing touches for now

Looking at the game scene, something still seemed off. The character is meant to be floating in the air but there was no way to tell. This is because there is nothing to visualise where the player is. Many 2D games, including Stardew Valley, fix this problem by putting a shadow beneath the character’s feet to generate depth within the 2D plane. This was my original solution as well, however, one slight problem. My artistic direction swapped legs for a fire based thruster. 

While games don’t always have to make sense, like tell me why I can fit 40 sharks in my pockets in Animal Crossing New Horizons, some elements do for an immersive effect. Putting shadows directly beneath a flame (a light source), breaks physical immersion inside a videogame. With that thought, the shadow solution is no longer on. My next thought was a burn trail. This could leave a short trail behind the character, which also breaks immersion as materials don’t magically get rid of burn marks, and permanent burn marks will essentially hide the art which makes up the world. So taking inspiration from the shadow, I created a simple animation of a ring of fire, to highlight the exact position of the player in an immersive way.

!["Final verison of the character for now"](/Recordings/3.6/recording3.mp4)

Now we have something to mark the position of the player, we might as well ensure the player interacts with the world correctly before moving on. To do this, a CollisionShape2D node is needed, which will act as a hitbox limiting where the player is able to go. To create the hitboxes for the walls, a Physics Layer is created, allowing for each tile within the tile set to hold a custom hitbox, which interacts with the ring of fire.

The last thing needed to be done here is “y-sorting”. This dictates whether Godot should draw a sprite behind or in front of an object by comparing y-values with the sprite (default value is 0). A tutorial and some funny attempts (with the character fully disappearing) later, y-sorting has been solved, creating more immersion as the player scene is partially hidden behind the bottom wall. 

With all of that done, the initial design of the protagonist is finished. While it is mute, the only logical sound effect so far would be a flamethrower. This will not be implemented as a constant stream of a repetitive sound will become stale quickly. A sound system will be dealt with later.

The one final touch I want to add to the protagonist’s character is random intervals between the blinks. I could just use the random class Godot offers, but I have something special planned. 
