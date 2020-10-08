# Exercise-04b-Hide-and-Seek
Exercise for MSCH-C220, 8 October 2020

This exercise is designed to continue our creation of a 2D Platformer, by creating and experimenting with two enemy types. The concepts behind this exercise will be outlined in class.

Fork this repository. When that process has completed, make sure that the top of the repository reads [your username]/Exercise-04b-Hide-and-Seek. *Edit the LICENSE and replace BL-MSCH-C220-F20 with your full name.* Commit your changes.

Clone the repository to a Local Path on your computer.

Open Godot. Import the project.godot file and open the "Hide and Seek" project.

You should see a very basic 2D Platformer with tiles made from the Godot Logo. The player is very similar to the one we developed in exercise 04a. *Notice he now jumps with the w character instead of the space bar.* Now, we will create some enemies for him to contend with.

In the Scene Panel, right-click on the Enemy_Container node and Add Child Node. Select KinematicBody2D, and rename it Bat.

As children of the Bat node, add AnimatedSprite, CollisionShape2D, and RayCast2D nodes.

Select the AnimatedSprite. In the Inspector Panel, select Frames->New SpriteFrames. Then select Frames again, and choose Edit.

The Animate Frames panel should appear at the bottom of the window. Editing the default animation, press the Sprite Sheet icon and choose res://Assets/bat.png. All three of the images should be included in the default animation.

In the Scene panel, select the Bat's CollisionShape2D. Create a CircleShape2D collision shape with a radius of 10.

Now add a script to the Bat. Save it as res://Enemy/Bat.gd:

```
extends KinematicBody2D

var player = null
onready var ray = $RayCast2D
export var speed = 250
export var looking_speed = 100
	
func _physics_process(delta):
	if player == null:
		player = get_node("/root/Game/Player_Container/Player")
	else:
		ray.cast_to = ray.to_local(player.global_position)
		var c = ray.get_collider()
		if c:
			var velocity = ray.cast_to.normalized()*looking_speed
			if c.name == "Player":
				velocity = ray.cast_to.normalized()*speed
			move_and_slide(velocity, Vector2(0,0))
```

Test the game, and watch the bat's behavior. Notice how it flies faster when it has a clear line of sight to the player.

Now, here's a task for you to figure out. When the bat touches the player, we would like the player to die. Hint: I would recommend using an Area2D node with a circle shape larger than the bat's collision shape. The player has a .die() function you can call.

I have created a Turret scene that uses a state machine to cycle through three different modes: scanning, searching, and found. Instance and place four turrets in the scene as children of the Enemy_Container node (note, if the turret can see the player's starting position, it will kill it continuously). You can rotate and place them on the ceiling, walls, or floor.

Take a look at the Turret scene. Do you understand what is happening? What questions do you have? How might you want to modify it in the future?

Test the project. You should now see the turrets cycling through their modes.

For extra credit, add the following states to the Player state machine: attack, crouch, and die (the die() function in the player can instead update the state machine). You can add animations for the states, as they are available. Can you implement double jump or wall jump? How would you do that?

If you implement any of the extra credit, describe what you did in the README.md, below.

Quit Godot. In GitHub desktop, add a summary message, commit your changes and push them back to GitHub. If you return to and refresh your GitHub repository page, you should now see your updated files with the time when they were changed.

Now edit the README.md file. When you have finished editing, commit your changes, and then turn in the URL of the main repository page (https://github.com/[username]/Exercise-04b-Hide-and-Seek) on Canvas.

The final state of the file should be as follows (replacing the "Created by" information with your name):
```
# Exercise-04b-Hide-and-Seek
Exercise for MSCH-C220, 8 October 2020

THe second exercise for the 2D Platformer project, exploring two enemy types.

## Implementation
Built using Godot 3.2.2

The player sprite is an adaptation of [MV Platformer Male](https://opengameart.org/content/mv-platformer-male-32x64) by MoikMellah. CC0 Licensed.

The bat sprite was originally created by bagzie for Stendhal and was [reworked by AntumDeluge](https://opengameart.org/content/bat-rework). 

## References
None

## Future Development
None

## Extra Credit
None

## Created by 
Jason Francis
```
