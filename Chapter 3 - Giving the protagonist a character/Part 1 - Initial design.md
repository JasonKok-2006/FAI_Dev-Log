## 3.1 – Giving the protagonist a character - Initial design

As already established in FAI Dev-log 2.1 (Starting to draw a world - Art direction), pixel art allows for quick designs for the spritemaps used for FAI. However, while the 16x16 pixel tile size works for tilesets related to the world, I chose to give a tileset size of 32x32 for the protagonist. Then by splitting the character into 3 sections (head, body, thruster), I can group each part together to form the protagonist. This saves having to draw every combination and also splits the logic for the correct animations which simplifies the program’s logic, which allows me to easily edit the file if I have to in the future.

The reason why 32x32 pixel size was used for the protagonist was solely due to the head portion of the character. If I used 16x16 pixel size for the character, the facial expressions become rather limited due to the space that would be given to the eyes and mouth (4x2 compared to the 8x4 that a 32x32 pixel size allows). As I also previously mentioned in FAI Dev-log 2.1 (Starting to draw a world - Art direction), I am a novice artist. Hence, the character is a limbless robot making it easier to draw and animate for me as I improve my artistic capabilities. This means to stop the protagonist feeling lifeless, the only option is to majorly enhance the facial expressions giving the protagonist personality. 

All in all, putting the character together, I'm pretty happy how it looks once its in the Godot scene.

![The initial design of the character](/Screenshots/Chapter3/3.1/Initial.png)