## 4.2 – Determinising randomness - Optimised Implementation

Videogames have to run smoothly for them to be enjoyable. Often at times, great games such as “The Legend of Zelda: Breath of the Wild” have been criticised for frame drops in certain parts of the game such as “Korok Forest”. Even though the game is positively received in general, frame drops within games will always be negatively critiqued. 

Say a game has a target frame rate of 60fps (frames per second). Every maths, physics and visual update within the active scope has to be completed before the game can update to its next frame. This means everything that makes up the game has to be updated within ~0.016 seconds for the game to run smoothly. This highlights the definite need for optimisation within the project as slow algorithms can lead to a slower game. 

This is where time and space complexity come into play. Both complexities measure the efficiency of an algorithm, with time complexity affecting frame rate and space complexity affecting RAM usage. To simplify the complexity, big O notation tells us how much an algorithm’s efficiency declines with larger inputs. 

![Big-O graph](/Screenshots/Chapter4/Part2/1_5ZLci3SuR0zM_QlZOADv8Q.jpg)
*Credit to this website https://medium.com/swlh/basics-of-big-o-notation-7d5d905d058d*

In the last FAI Dev-log (4.1 – Determinising randomness - Outlining the PRNG), the PRNG was outlined into how it would work. Now as a basic coding exercise, implementing the intuitive way is not always the best way. A function like this is correct but it has an O(n) complexity. 

```csharp

// This is the version that is called in every other script
public static int GenerateNewRandomNumber(int p, int g, int x)
{
    return GenerateNewRandomNumber(p, g, x, 1); // Helper solely to elinate the addition of the 4th argument.
}


// Previous unoptimised verison
public static int GenerateNewRandomNumber(int p, int g, int remaining_x, int current_y)
{
    if (remaining_x <= 0) // reached the end of the exponential sequence
    {
        return current_y; // return the final result
    }

    int updated_y = (current_y * g) % p; // One step in the exponential process
    return GenerateNewRandomNumber(p, g, remaining_x - 1, updated_y); // recursively call decreasing a step
}

```

After a little research to look for optimisations, a fast calculation method (known as fast exponentiation) provides an O(log n) complexity. This means if the value for x (the exponential) is a 1000, we can calculate the result in ~10 calculations compared to ~1000 needed before. More extreme examples will provide a more significant time save when using this function, allowing the use of larger values as it won't affect the overall performance of the game.

```csharp

// This is the version that is called in every other script
public static int GenerateNewRandomNumberInt(int p, int g, int x)
{
	int currentTotal = 1;
	int previousIndex = 0;
	int previousValue = g;
	int moddedX = x % p;

	char[] binaryx = Convert.ToString(moddedX, 2).ToCharArray(); // take the binary of x
	Array.Reverse(binaryx); // reverse it

	for (int i = 0; i < binaryx.Length; i++)
	{
		if (binaryx[i] == '1')
		{
			int indexValue = FastModExponential2(p, previousValue, i, previousIndex); // Get the mod value for that specific power.
			previousValue = indexValue; // Update the previous value variable so the fast mod function works for the next iteration. 
			previousIndex = i;
			currentTotal = currentTotal*indexValue % p; // multiply the index againt the current total
		}
	}
	return currentTotal;
}

public static int FastModExponential2(int p, int y, int i, int lasti)
{
    if (lasti < i) // lasti is used as savepoint. This will optimise this function by reducing average tiem complexity of O(n) to O(1) (n being length of binary string)
    {
        int newy = y*y % p; // Calculate the value of the next largest power of 2
        return FastModExponential2(p, newy, i, lasti+1); // Recursively call if we dont have the correct exponential 
    }
    return y; // y holds the correct result
}

```