## 2.3 – Starting to draw a world - Zooming in

As mentioned in the previous FAI Dev-log (2.2 – Starting to draw a world - Creating the initial scene), when I pressed F5, the room was tiny compared to the game screen. This could be fixed by just making the room larger, but this means larger sprites would be required for the characters to make the game enjoyable for the player. I mean as a gamer myself, I wouldn’t want to be squinting at the screen to see what is going on. 

So to fix the tiny room situation, we need a way to zoom into the scene. This is where the Camera2D node comes in. By adding this node, the game screen now snaps to the scope inside the camera box rather than the default scope that the scene normally has. As this scope is customisable, I am able to customise the scope that the camera sees by changing parameters such as position and scale. By increasing the scale, the scene zooms in and the problem is fixed. 

![Attempt 2](/Screenshots/Chapter2/2.3/take2.png)

However, something still seems off about the room. 
