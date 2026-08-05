## 5.1 – Meet FAI - Trigger warning

Every game needs some objective for the player to work towards. In the case of Stardew Valley, it's initially rebuilding the community centre. In the case of Minecraft, an open world sandbox game, it’s defeating the Ender Dragon. 

In the case of FAI, it’s collecting data for **FAI (Fragmented Artificial Intelligence)**, directly taking inspiration from the work I was doing for DataAnnotation for over a year now. The data collection goals are going to work like Stardew Valley community centre and Animal Crossing series' museum, which takes a chore-like task and makes it fun and rewarding. 

Before we implement FAI, we need a way to activate him, some sort of trigger. Well FAI can’t be activated constantly, it’s a software which means we need some hardware to support it. A screen and well … the player character. 

To activate the screen, we need something to turn it on. Something obvious to which a player can tell they should activate. A pressure plate. 

This can easily be done with a new TileMapLayer node which displays the pressure plate and an Area2D node. Area2D nodes have built in signals which can be used to trigger functions when colliders enter and leave the defined area. By creating a script where the tileset gets swapped out when the player steps on the trigger and swaps back to the default when the player steps off the pressure plate, the problem of making an interactive pressure plate is solved.

Well with the trigger set up, visually warning the player about activating FAI, the next step is to implement the character.

![Showcase of the pressure plate](/Recordings/5.1/TriggerCreated.mp4)