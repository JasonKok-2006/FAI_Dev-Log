## 3.4 – Giving the protagonist a character - Visualising energy

The last FAI dev-log (3.3 – Giving the protagonist a character - Nothing to show) mentioned that there was no visual representation of the health system. So before we move on to the next thing to implement, let’s finish the energy system. To do this, we need a CanvasLayer option in the main game scene. A canvas layer size snaps to the game screen size, allowing any Control (UI) nodes to be repositioned and rescaled to what the current game screen is. This ensures consistent UI layouts between different devices that have different screen resolutions. 

The energy bar is made by using a TextureProgressBar. This node provides fields for ‘Under’ (the background sprite), ‘Over’ (the foreground sprite) and ‘Progress’ (the sprite between which the percentage shown is based on the node’s value) textures. For the energy bar, a battery outline is used for the ‘Under’ sprite and a basic white shape fill is used for the ‘Progress’ sprite. The ‘Over’ sprite is left at null. 

Now we have a representation of energy added to the main game scene, we need a way to display the correct values. First problem, the character is in its own scene, therefore we need to ensure that the main scene has access to the player scene’s values. What seemed like a hard task initially, was made trivial after some research. By ensuring the root node of the player scene has the script controlling the scene (the player in this case), we can attach the same script to the imported player scene in the main scene. This means any variables we need can now be accessed between scenes.  

Now that we have access to the player script from another scene, we have something to think about. The game state updates every frame. However, the current energy system at the moment decrements the energy every 0.5 seconds. With the target frame rate at 60 frames per second, it means for every second 2 out of 60 frames have an energy level change. So if we update energy levels in _PhysicsProcess, such that the health bar gets updated every frame, we have 58 frames per second of unnecessary updates. This can be solved by creating a custom signal and updating the health bar once the custom signal has been emitted. Signals allow for data to be transferred between scenes without the other scene having to look within the other scene’s script, as the emitter can send out temporary values any receiver can read from. By using signals, we update the health bar visual only when there is a health change, eliminating 58 unnecessary updates per second. 

```csharp
private const int GREEN_RANGE = 70;
private const int AMBER_RANGE = 30;
private const int BLUE_VAL = 40;
private const int ALPHA_VAL = 255;
private const int MAX_RGBA_VALUE = 255;

public void CalculateTint(int currentEnergy, int fullEnergy)
{
	int batteryPercentage = (currentEnergy * 100) / fullEnergy;
	int redVal;
	int greenVal; 

	if (batteryPercentage >= 30)
	{
		redVal = MAX_RGBA_VALUE - (((batteryPercentage - 30) * MAX_RGBA_VALUE) / GREEN_RANGE);
		greenVal = MAX_RGBA_VALUE;
	}
	else
	{
		redVal = MAX_RGBA_VALUE;
		greenVal = (batteryPercentage * MAX_RGBA_VALUE) / AMBER_RANGE;
	}

	EnergyBar.TintProgress = Color.Color8((byte)redVal, (byte)greenVal, BLUE_VAL, ALPHA_VAL);
}
```

By using a solid white fill for the progress texture, RGBA tint values can be calculated based on the battery percentage that the player currently has. This allows for smooth colour change as the player’s energy depletes adding a sensible additional visual cue to the player, warning them that their time is running out.

![Energy bar visual recorded](/Recordings/3.4/recording2.mp4)