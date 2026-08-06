## 4.3 – Determinising randomness - Putting it to use

Back in FAI Dev-log 3.6, I mentioned I wanted to make the character blink in random intervals. So, let's do that!

Slight problem though. The current custom API we made doesn’t support ranges. Ranges are required in this blinking scenario because when a human blinks naturally, very rarely they will have to blink again a second later, so we can eliminate small numbers like 1, 2 or 3. So we need a way to take the number we have from the range between 1 and p-1 into a custom range. Well, to do that, we can just use this function:

```csharp
// Variation for a range between the min and max
    public static int GenerateNewRandomNumberInt(int p, int g, int x, int min, int max)
    {
        int range = max - min;
        float result = GenerateNewRandomNumberFloat(p, g, x);
        return (int) MathF.Round(result * range) + min;
    }
```

Where we find the float result and multiply that by the range. Adding the minimum value in the range guarantees a value generated between the specified min and max arguments.

Before we use this API, testing has to occur. Enough testing has to be done to ensure that the formulas have been programmed successfully. This is where unit testing comes in. A script containing many test cases which when executed, compares the API results to the expected results. Once enough test cases have been made and they all pass, we can guarantee that the API works as expected (creating seemingly random values).

So back to the character’s blinking problem. This can be solved by choosing the min value 4 and the max value 9, where the intervals for blinking are seemingly random. The value of p is 67 and the value of g is 50 (no reason for these specific values). The value of x is determined from when the player starts the game, how many times the player has blinked so far. A variable keeps track, incrementing by 1 every time the player blinks, so a fresh result is called each time from the API. 

No player controlled actions can affect this interval. While I specifically designed the PRNG this way so the player can affect randomness, some niche random elements within the game really does not need a player input!
