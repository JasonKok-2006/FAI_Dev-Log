## 5.2 – Meet FAI - On screen

So we have a screen for FAI and a button to activate it. Now, we have to get some response from FAI. To make a solid fill to turn the screen on, a rescaled 1x1 pixel is revealed when the player steps on the trigger. 

Considering FAI is a character based on LLMs, let's make a text generation animation, where extremely low poly text is displayed to FAIs screen to match the dialogue box planned for later. 

To do this, take the 1x1 white pixel sprite and modulate it to display a black version. Once one iteration of the sprite can be created and destroyed, loops can be used to display more iterations. Taking the position of FAI within the scene and taking the positions/lengths of FAI, the correct position of the sprite can be calculated. Keeping track of how far along the line the script is, if the sprite still fits on the line it gets placed and if not then the sprite goes onto a new line. 

Multiple sprites can be handled within a Queue. A First-In-First-Out data structure along with a custom struct which only contains a Sprite2D field (the word sprite) and an int field (the current row of the sprite). This allows a scrolling effect within the animation, as the Queue gets reset decrementing all previous sprites by 1 and the position gets recalculated based on the new row. If the new row is -1, then the sprite is never re-enqueued and gets deleted. 

Due to the sprite being created by the script, the automatic pivot point of the sprite is in the middle. This has to be kept in mind with the positioning of the sprite, where the sprite gets placed at the X position, half a sprite length away from the position we want to actually add it to. 

![FAI's sreen made](/Recordings/5.2/FAI%20Screen.mp4)