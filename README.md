# The RPG Maker MV Spriter Plugin v.1.3.5 by KanaX
https://forums.rpgmakerweb.com/index.php?threads/spriter-plugin.90340/

# Introduction
Allows user to utilize Spriter Pro save files and sprite parts for Skeletal Animations

# Features
Using Spriter, it is easy to create functional, fluid, expressive animations with sprite parts, without needing to create large numbers of sprite sheets.
Additionally, Spriter Plugin allows you to manipulate your new Spriter sprites and give them special functions like:
Moving sprite in slow-mo, or fast-forward.
Change the bitmaps of a sprite so that the same animation is done with a different visual character.
Example: Change skin set from a man to a woman, doing the exact same movement.
Change/add new parts to your existing animation.
Example: Add hat to character / Change hair of character.
Add sound effects according to the animation cycle.
Example: Footstep, every time the character's foot lands their foot down.

# Videos
Here's a little story created with Spriter Sprites (View in 720p and fullscreen for better experience)
https://www.youtube.com/watch?v=tXtpVi5LKy0

Here's the same video with labels explaining what happened where:
https://www.youtube.com/watch?v=OTXT85O_1Ms

A display of Spriter Sprites:
https://www.youtube.com/watch?v=yDvTDZL2dv4

A display of Bones, the moving parts that sprite pieces "stick" on.
https://www.youtube.com/

The animation when it is in Spriter:
https://www.youtube.com/watch?v=aw51G-Jmly4

How to Use
Spoiler: Click Here
Installation:
Paste js file in js/plugins/
Create path img/characters/Spriter/ and inside Spriter, a folder named Single Bitmaps.
Paste SpriterObjects.json in data/ or copy the one from the demo.
Create path data/animations/.
Enable the plugin from the Plugin Manager and assign a number for the variable which will store animation info.
WARNING: Do not modify that variable after activating the plugin.
Have some ramen noodles, because you deserve them.
Regarding Spriter:
The plugin should work as expected in most regards (please check "Future Updates/Fixes" for more information).
The first 4 animations in a Spriter project will respond to the character's 4 directions. If you want your character to move without Direction Fix, you have to create at least 4 animations.
While you can change the pivot of your bitmaps when you have inserted them into your project, you must not edit pivot x and pivot y in Edit Image's Default Pivot
Spriter might face some problems with its documentation, so if something inexplicably does not work, try redoing the animation. If that does not fix your problem, feel free to contact the plugin creator.
Plugin Operation:
Paste Spriter Pro save file in data/animations/. The file name will be the skeleton,
Create a folder in img/character/Spriter/, named after the Skinset. The Skinset folder should have 4 folder which each taking the parts for each direction.

Example:
Folder_1: [head,torso,r_arm,_r_leg,_l_arm,l_leg],
Folder_2: [head,torso,r_arm,_r_leg,_l_arm,l_leg],
Folder_3: [head,torso,r_arm,_r_leg,_l_arm,l_leg],
Folder_4: [head,torso,r_arm,_r_leg,_l_arm,l_leg]

Note: If you use TexturePacker spritesheets, instead of creating folders for each direction, just place in the Skinset folder the .png spritesheet and the .json file. Make sure to name them the same as the Skinset folder. Step 3 is also null.

Inside the Skinset folder, create the folders with the bitmaps you used for the animation.
If you want certain Spriter Sprites to appear globally across the game (such as animated armor and weapons for actors) you need to create them in the SpriterObjects.json file in your data folder. (See more info about SpriterObjects.json in About SpriterObjects.json).
To create a Spriter Sprite for actors, go to Tools -> Database and write this on the actors' notes:
<Spriter:{
"_skeleton": The file name of the animation you want to choose from data/animations/,
"_skin": The folder name of the Skinset you want to choose from img/characters/Spriter,
Note: If you use TexturePacker spritesheets, add a "$" in front of the skin name.
"_speed": Speed of animation,
"_cellX": Width of the area the main animation takes part in (example: the standard MV character cell width is 48),
"_cellY": Height of the area the main animation takes part in (example: the standard MV character cell height is 48),
"_spriteMask": Determine if the sprite will have a mask around it. If true, you need to fill the tags below,
"_spriteMaskX": X value of mask origin. 0, 0 is the top left corner of the cell,
"_spriteMaskY": Y value of mask origin. 0, 0 is the top left corner of the cell,
"_spriteMaskW": Width of the mask,
"_spriteMaskH": Height of the mask
}>

Example:
<Spriter:{
"_skeleton": "female_running",
"_skin": "female4",
"_speed": 4,
"_cellX": 48,
"_cellY" : 48,
"_spriteMask": true,
"_spriteMaskX": 0,
"_spriteMaskY": 0,
"_spriteMaskW": 48,
"_spriteMaskH": 48
}>

To create a Spriter Sprite for an event create a comment in the active event page:
<Spriter, skeleton, skinset, speed, cellX, cellY, false>
or
<Spriter, skeleton, skinset, speed, cellX, cellY, true, maskX, maskY, maskW, maskH>

Example
<Spriter, doggo, sheperd, 10, 48, 32, true, 0, 0, 48, 32>

WARNING: 01/24/2018 THERE IS A PIXI.JS BUG IN v4.5.4 THAT MAKES MASKS NOT WORK IF THE MAP HAS TILES.

Animations play when 1) an actor/event has walking animation on and is moving, or 2) an actor/event has stepping animation on.

For animations that are supposed to loop (walking animations, rolling balls, etc.), you need to toggle the Repeat Playback button in the Spriter Pro timeline.

About SpriterObjects.json

Much like the MV Sprite_Character class, Spriter_Character class looks for data in the actor/event object in order to create/update a sprite. But what happens when we want our character to hold an animated sprite? A sprite whose animation is separate from the animation of its parent? Like a torch, or a magic aura. And what do we do when we want to keep these sprites for multiple maps?

That's why we create SpriterObjects!

In SpriterObjects we create faux game objects, with just the bare minimum data to satisfy the needs of the Spriter_Character class. You create a new object, you give it a name, skeleton, skin and then you can attach it to any character you want!
These objects are created as comments in the COMMON EVENT with the ID that you assigned on the Spriter Objects Common Event ID:

<objectName, skeleton, skin, speed, cellX, cellY>

Plugin Commands:
eventSkeleton eventId data/animations/skeleton Spriter/skinsetName
(Changes skeleton. Since skeleton changes, skinset needs to change as well.)
Example: eventSkeleton 1 waving_hello male_1

eventSkin eventId Spriter/skinsetName
(Changes Skinset. Needs to be compatible with skeleton.)
Example: eventSkin 1 male_2
Note: For TexturePacker spritesheets, add a "$" in front of "male_2"

eventStop eventId true/false
(Stops Animation.)
Example: eventStop 1 true

eventRecovery eventId ("snap"/"freeze")
(Snap resets animation when movement stops. Freeze pauses animation.)
Example: eventRecovery 1 freeze

eventSkinPart eventId imageName (Spriter/skinsetName)-or-(bitmap name from Single bitmaps) fullsprite?
(Changes only a single image from that skinset to another, compatible one. fullsprite is set to true or false and determines if the new bitmap will be from a full spriteset or not. If it is set to true then the user will have to use the desired spriteset path. If it is set to false then the user will have to use the desired bitmap path from within the Single Bitmaps folder)
Example1: eventSkinPart 1 hat Items/helmet true
(helmet needs to be a folder with the same filename/location as the one of the previous bitmap)
Example2: eventSkinPart 1 r_hand_weapon mace false
(mace needs to be a bitmap inside the Single Bitmaps folder)

Note: For TexturePacker spritesheets, add a "$" in front of "Items/helmet"/"mace"

eventRemoveSkinPart eventId imageName
(Removes Spriter/skinsetName bitmap from imageName)
Example: eventRemoveSkinPart 1 r_hand_weapon

eventChildSprite eventId imageName objectName
(Assigns a sprite from data/SpriterObjects.json to imageName)
Example: eventChildSpriter 1 r_hand_weapon glowing_mace
(glowing_mace needs to be an object in SpriterObjects)

eventRemoveChildSprite eventId imageName objectName
(Remove sprite object)
Example: eventChildSpriter 1 r_hand_weapon glowing_mace

playerSkeleton data/animations/skeleton Spriter/skinsetName
playerSkin Spriter/skinsetName
playerStop true/false
playerRecovery ("snap"/"freeze")
playerSkinPart imageName Spriter/skinsetName
playerRemoveSkinPart imageName
playerChildSprite imageName objectName
playerRemoveChildSprite imageName objectName
followerSkeleton followerId data/animations/skeleton Spriter/skinsetName
followerSkin followerId Spriter/skinsetName
followerStop followerId true/false
followerRecovery followerId ("snap"/"freeze")
followerSkinPart followerId imageName Spriter/skinsetName
followerRemoveSkinPart followerId imageName
followerChildSprite followerId imageName objectName
followerRemoveChildSprite followerId imageName objectName
Script Calls:
$gameMap._events[1].resetAnimation = true;
(Resets animation)
$gamePlayer.resetAnimation = true;
$gamePlayer.followers()[1].resetAnimation = true;
$gameMap._events[1].hasActiveTag("tagName");
(Checks if character has an active tag for this frame)

$gameMap._events[1]._spriter.var.variableName
(Returns value for variableName for this Frame)
Tag Commands: (Place tags on Spriter with the following labels for special effects)
se,seName,pan,pitch,volume,fade(, areaOfMaxVolume, areaOfTotalFade)
(Plays SE sound. If fade is true, the sound fades away the further the player is from the source)
Example1: se,step,0,100,60,true,3,10
Example2: se,clock,0,80,100,false

SkinPart,imageName,(Spriter/skinsetName)-or-(bitmap name from Single bitmaps),fullsprite?
(Works exactly like the plugin command. Useful for automatically spawning sprites with certain skinParts. Not so useful if those sprites change parts often.)
Example1: SkinPart,hat,stink_lines,false
Example2: SkinPart,torso,Items/tuxedo,true

RemoveSkinPart,imageName,(Spriter/skinsetName)-or-(bitmap name from Single bitmaps),fullsprite?
Example: RemoveSkinPart,hat,stink_lines,false

ChildSprite,imageName,objectName
(Works exactly like the plugin command.Useful for automatically spawning sprites with certain childSprites. Not so useful if those sprites change children often.)
Example: ChildSprite,r_hand_tool,twinking_axe

RemoveChildSprite,imageName,objectName
Example: ChildSprite,r_hand_tool,twinking_axe

Tutorial: https://www.youtube.com/watch?v=KiJ2iqbxc0g&list=PLdAT_cKw4gBhvP3rvwMAzQ9D3GhtolmUA

Credit and Thanks
Free for use in all projects.
Please provide credits to KanaX.
Feel free to let me know about your project, or any ideas regarding the plugin.
Special Thanks to ivan.popelyshev (https://github.com/pixijs/pixi-display/tree/layers)

Future Updates/Fixes
Fix reverse animations (this._speed < 0).
Add ability to distort texture meshes.
Make functional masks after dealing with a pixi.js bug.
Author's Notes

I hope this contributes to the community that helped me substantially with my growth!
It is my first official plugin so feel free to recommend any changes, fixes, suggestions, offer criticism, etc.
UPDATE: If you are interested in using Spriter Plugin in a battle scene, feel free to contribute in this poll.

02/22/2018: Fixed Subfolder Issue of RPGMV version 1.6
03/18/2018: Added:
Performance Boosters
Bezier Curve Tweening for Animations
Instant Tweening for Animations
TexturePacker Support
04/30/2018:
Fixed saving issue.
Replaced bitmaps with textures.
Tweaked the core of the plugin to work with up-coming Battle_Scene add-on.
With tagging certain sprites can automatically change their skin according to their equipment.
