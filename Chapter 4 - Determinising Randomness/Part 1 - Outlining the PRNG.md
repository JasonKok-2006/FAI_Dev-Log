## 4.1 – Determinising randomness - Outlining the PRNG

Randomness exists in games to keep a game fresh over many playthroughs. It’s a way to stop the player from strategising the whole game beforehand and forces them to adapt to the situation. Take a game like “Mike Tyson’s Punch-Out!!”, randomness within each fight forces the player to react to each attack rather than eventually memorising a set of inputs, preventing the 14 fights within the game from becoming stale. While randomness boosts enjoyability in the game for the average player, it can negatively impact the speedrunning scene when too many random elements will make or break a speedrun outside of the player's control. 

I myself am very fond of the speedrunning scene in videogames. Having achieved the world record time on some levels found in the “Popular” menu in “Super Mario Maker 2” along with speedrunning many games casually, I love the idea of the speedrunning community coming together to push a game to its limit. So when random elements dictate a time loss near the end of a run, it becomes very frustrating. That’s why within FAI, all supposedly random elements will be generated using a Pseudo-Random Number Generator (PRNG), which certain actions from the player will affect the outcome. This allows for speedrunners to map out certain routes within the game to push the game to its limit while keeping the game seemingly random for casual players.

So, we need a formula to do this. Taking inspiration from the Diffie-Hellman (DH) key exchange, a cryptographic method primarily used to exchange secret keys over a public network, seemingly random integers can be generated. The formula is as follows:

**y = g^x mod p (g to the power of x)**

By choosing a suitable value for both p and g, along with a value for x which is calculated through a mix of player controlled actions and general incrementations, a seemingly random integer between 1 and p-1 will be generated. By calculating the value of y this way, the player will be able to control elements in the game in a stable manner as the framework p and g values aren’t affected by the player. Instead, the p and g values will be selected based on the scenario. To turn the integer given into a float (if needed), the formula used will be:

**float = y / p**,

Which also signifies the importance of choosing a suitable value for p. This will generate a float between 0 and 1. 

An added benefit to this randomness system is predetermined values can allow for quick testing. Instead of waiting for the random event to happen, manipulating the values beforehand allows for the game to be tested with all outcomes quicker without having to implement an extensive cheat code system to manipulate the randomness. 
