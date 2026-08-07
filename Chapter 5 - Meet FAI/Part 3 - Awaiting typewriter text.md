## 5.3 – Meet FAI - Awaiting typewriter text

So now we have an animation that plays when FAI is telling us something, it’s time to add a dialogue pop-up to the trigger. To do this, a function is attached to the trigger’s signals which plays the animation revealing the Panel and RichTextLabel nodes when needed. 

To make sure the dialogue fits within the scenes in the game, a custom pixelated font was created for this game. However, due to licensing issues within the software I used to create the font, I couldn’t use the font I created if it’s in a sold product. So for now (to save another afternoon’s worth of work), an open-sourced font package is being used. I hope to change this back to my custom font I made at some point in the future when redesigning the art but for now, I’m just going to use the open-source font and move on.

Playing Stardew Valley, the character’s dialogue reveals one letter at a time. This is known as the typewriter effect, which is a common work around games to eliminate throwing too much to the player at once. To reveal one letter at a time, we need to dynamically create a timer, which when finished a character is revealed and the next character is revealed. This can be easily done as RichTextLabels have a VisibleCharacters parameter which reveals the amount of characters specified. 

However, this is where the async and await keywords come into place. The async keyword marks the function such that when it is paused, the main thread does not get blocked. The await keyword pauses the execution of the function until the task has finished (in this case is the timer’s Timeout signal being activated). Together, this allows the typewriter effect to play smoothly. 

Create a dummy dialogue text, hit play and it works!

![Typewriter Text Showcase](/Recordings/5.3/Video%20Project%209.mp4)