## 2.4 – Starting to draw a world - What seemed off, now seems on

As mentioned in the previous FAI dev-log (2.3 – Starting to draw a world - Zooming in), something seemed off about the initial room. 

![Attempt 2](/Screenshots/Chapter2/2.3/take2.png)

So I went to my inspiration for this project, Stardew Valley. I booted up my Nintendo Switch and loaded up my file I reached perfection on and started playing. Walking around the house, I realised an obvious thing. To create this perspective of top down (but not fully birdseye), the bottom wall has to cover the floor slightly. This fix needed some new tiles which I had to draw.

Walking around the house in Stardew Valley a little more, I noticed slight shadows along the walls. While they were not massively noticeable at first, they help distinguish the walls from the floor in a natural way. So let’s add them! To do this, again new sprites would be created to represent the shadows. Adding a new TileMapLayer node for the shadow sprites I positioned the shadow layer so Godot displays the ‘Ground’ layer first, ‘Shadow’ layer second and the ‘Wall’ layer last. However, this led to a slight problem, LibreSprite (the application I used to create the sprites) uses RGB (Red, Green, Blue) values. This means no degree of transparency was offered, leading to the shadows being a solid black sprite. 
 
The fix for this is making use of Godot, as it offers a variety of options to customise the node, including RGBA (Red, Green, Blue, Alpha) values. This is found in the node’s Inspector > Visibility > Modulate. RGBA adds the ‘Alpha’ parameter, which decides the opacity of the object (0 for fully transparent - 255 for fully visible). By adjusting the RGBA values of a TileMapLayer, the sprites can become darker than the original import, be given a coloured tint, and also become more transparent. The default RGBA values are (255, 255, 255, 255) which provides a white lighting (default sprite) and fully opaque. By reducing the ‘Alpha’ value, a solid black edge can be turned into a translucent shadow. 

With the aim to make the room have a dystopian feel, the flooring felt too light. Hence by lowering the ‘Red’, ‘Green’ and ‘Blue’ values on the RGBA value for the ‘Ground’ TileMapLayer, the floor becomes darker, saving me from redrawing the ground sprites. 

![Attempt 3](/Screenshots/Chapter2/2.4/finished.png)

With all that, we now have an empty room which is ready to go. Now what’s missing is a character which the player can control. 
