This is version 1 of the upgraded Augmented Space Library (ASL). It is being built with Unity 2019.3.3f and Amazon Web Services - GameLift RealTime Servers (https://docs.aws.amazon.com/gamelift/latest/developerguide/realtime-howitworks.html). 

Documentation for this framework can be found here: https://uwb-arsandbox.github.io/ASL_Master/ASLDocumentation/Help/index.html The first page of website is shown below.

<html>
	<head></head>
	<body>
		<h1>Augmented Space Library Documentation</h1>
		<p>Welcome to the Augmented Space Library (ASL) Documentation System. Here you will find documentation on how ASL works so you can futher improve its functionaility, as well as find documentation on demos within ASL to better understand how they work and how you can use ASL for your own multiplayer projects. </p>
			<h2>Getting Started</h2>
			<p>The steps to install and setup ASL are as follows:
				<ul>				
					<li>
						<p><strong>Download ASL</strong> - Download this project and open it in Unity 2019.3.3f1 (other verisions should work but are not guaranteed). If you have packages errors, then make sure you are using Unity 2019.3.3f1 or higher. If that still does not resolve your package issues, then  continue into Unity and then go to Help->Reset Packages to defaults. This should resolve any package errors.</p>
					</li>
					<li>
						<p><strong>Connect to other users</strong> - You will not be able to connect to others and will recieve errors if you do not have these scenes in your Unity build settings. Now, with that out of the way, there are two ways in which you can connect players to each other for either testing your application or using it. The first is through the use of the provided ASL_LobbyScene. If you use this method, you must ensure you always launch from this scene and include the name of the scene you want to launch to in its "AvailableScenes" dropdown UI object. The second method allows you to connect from whatever scene you want and is generally recommended as it involves less user steps. To use this method, you must attach the "QuickConnect" script to an empty GameObject and place that empty GameObject in the Unity Hierarchy window of your desired first scene at the very top so it execute first. You can see examples of this in all of the Simple Tutorials. You must also pick a unique room name and the starting scene for players to transition to after connecting and readying up with each other, the starting would ideally be the scene the QuickConnect script is located in, but does not have to be. If your room name is not unique, then you will join another ASL user's room. The starting scene can be the name of the scene you are currently working in. If you do use this method, you must still build the ASL_LobbyScene and ASL_SceneLoader scenes, though they no longer have to be built first.</p>
					</li>
					<li>
						<p><strong>Using ASL</strong> - You are now ready to begin programming a multi-user interactive experience! Refer to the documention if you are having trouble with any function, but in general, make sure to claim your object before doing anything with it and even then, the stuff you do with it should be ASL related only if you want others to see your changes.</p>
					</li>
				</ul>
			</p>				
			<h2>Adding documentation</h2>
			<p>Note, the steps to add to this documentation file are as follows, but note that SandCastle can be tricky at times.
				<ul>
					<li>
						<p><strong>Install Sandcastle</strong> -  Go here https://randynghiem.wordpress.com/2015/06/18/how-to-set-up-sandcastle-help-file-builder-with-visual-studio-2015/ and follow the steps provided. When you are actually installing SandCastle, install everything it desires.</p>
					</li>
					<li>
						<p><strong>Check the XML Documentation File Box</strong> - Right click in Visual Studios on "Assembly-CSharp" and go to properties. If nothing shows up then you need to allow Unity properties to be visible in Visual Studios. To do this, follow these directions: https://answers.unity.com/questions/1140063/cant-open-project-property-in-visual-studio-2015-w.html Once in the properties, go to build, and tick the "XML documentation file:" check box. An image of what it looks like can be found in the first link. WARNING: Rather annoying, everytime you interact with, run, or even focus on Unity, this file gets rewritten and this checkbox becomes unchecked. If you build SandCastle when this box is unchecked, no errors will appear, instead your documentation file will be blank.</p>
					</li>
					<li>
						<p><strong>Add Sandcastle to Visual Studio</strong> - Now that you have SandCastle installed and Visual Studio project properties set up, you need to add SandCaslte to your project. If the current documentation file (where you got this information from) is no longer available, then you'll need to add a new SandCastle project. To do this, right click your Solution in Visual Studios and Add New Project. Then select Documentation, Sandcastle Help File Builder Project. After adding this, go to the "Documentation Sources" folder and add "Assembly-CSharp.dll" which should also automatically add "Assembly-CSharp.xml", but if it doesn't, add it yourself. These sources by default will be found in "Temp\bin\Debug\" if you were able to successfully build your "Assembly-CSharp" project from Visual Studio. After adding this documentation sources, right click and build your SandCastle Documentation Folder. After this, just go to where it was built and go into the "Help" folder to find your documentation. If this documentation still exists and just needs updating, then instead of creating a new SandCastle project, just add this one instead (ASLDocumentation.shfbproj) and then build.</p>
					</li>
				</ul>
			</p>
			<p>For any additional help in installing, using, or modifying ASL, please contact Kelvin Sung.</p>		
			<h2>Final Notes</h2>
			<p>ASL allows you to have in sync objects (ASLObjects) in your scene before you start your scene and to instantiate these objects at run time. However, in order to ensure ASLObjects starting in your scene are synced properly across users they must have a unique name. This allows ASL to find these objects later and assign them the correct ASL ID. Techically, the formula used to help generate object uniqueness is based upon a string that combines the following: The object's name + the square root of ((the object's position, rotation, scale) + (the Dot Product of the object's rotation and scale * Vector.one)). The following string ends up being the object's name plus a number that is most likely unique, but not guaranteed. To ensure proper ASL object synchronization, give your ASLObjects that start in your scene unique names. ASLObjects instantiated during runtime do not need to have a unique name as their ids are created in a different fashion that is guaranteed to be unique and synchronized.</p>	
			<h3>AR Use</h3>
			<p>ASL currently (as of Decemember 2019) supports ARCore and its functionalities. If ARCore is not being used in your project, feel free to remove its SDK from your project. To do this, go into the Asset folder and delete "GoogleARCore" and "PlayServiceResolver". Doing so will prevent any ARCore demos from being able to execute. Currently, this includes all demos in "Assets/ASL_Tutorials/Complex/AR_CSS451_MP_Assignments" and "Assets/ASL_Tutorials/Simple/ARCloudAnchors". In general, ASL has the capability to synchronize all devices, however, ASL currently only has ARCore Cloud Anchors integrated. This means only Android AR devices will have the ability to have the same world origin to work from when in.</p>			
			<h4>AR Requirements</h4>
			<p>Besides your regular ARCore setup, https://developers.google.com/ar/develop/unity/quickstart-android, ASL requires you perform the following actions to ensure all users will stay in-sync. These actions relate specifically to Cloud Anchors which are required to ensure proper real-world orientation between users. There are two methods you can use. The first is to set the world origin for all users. if you choose this method, then every user will have the same world origin - something that is needed to ensure all objects remain in the same spot across users. The world origin, which is created via ASLHelper.CreateARCoreCloudAnchor(), should only set once (e.g., the world origin should never change once set). And, as with cloud anchors in general, should only be able to be set by one person. Whether this is done in code (by using GameLiftManager.Instance().AmLowestPeer()) or by another rule that you chose, it doesn't matter. The second method is to use just a normal cloud anchor and then to have your game objects be children of this cloud anchor. Doing so this way essentially replicates the world origin method, but this means only SendAndSetLocal____ functions will be able viable, as SendAndSetWorld____ may place objects in different locations on different devices due to the devices having different world origins. It should be noted that both methods can be used in tandem, but if you plan on setting the world origin at all, it must be done first - even before any objects are placed in the scene as they may not move properly after the world origin is set. However, sometimes it is easier to already have your objects in the scene upon start, rather than instantiate them at runtime. If your app is set up this way, then it is suggested you ensure the objects will not show up on the screen by giving them an initial position of 100 or higher, and then, after setting world origin, to move these objects with a SendAndSetLocal___ or World___ function. Doing so will then place all objects for all users in the appropriate location. This is the method the AR_CSS451_Mp2 scene uses.</p>
			<h3>Notes on Realtime Apps</h3>
			<p>If you check out "Assets/ASL_Tutorials/Complex/CSS385_MP_Assignments/Mp2/" you will notice that while all objects start in sync, due to the same random seed being used across all devices, the scene can quickly deteriorate as it is a realtime game with constantly moving parts that assume because they have the same code and same starting location will always be in sync. In order to synchronize this app completely, every object would need to move with a SendAndSet function and, more importantly, this would need to be handled by some "Host" like user, that processed collisions. Then other players would just send information specific about them. This model is the client-server model and is not the model ASL uses (we use the P2P model). Because of this, these types of applications are very hard for ASL to run efficiently. To help explain this better, ASL would be a very good library for a turn-based game, as each player could send its information and calculate what would happen on their own - still being in sync with other devices because they will calculate the same thing. Then they could release their turn and wait to recieve info. ASL would not be a good choice for a shooter game like the "Assets/ASL_Tutorials/Complex/CSS385_MP_Assignments/Mp2/" assignment because even though all objects start in the same position, due to internet speeds, it is possible that an instatiated object would miss a moving target on one device where it spawned in slow, but hit on another device because it spawned on time. Normally, for these types of games, there is a server to handle all of these interactions and then just pass on that information to its users - hit or miss, ensuring everyone stays in-sync. However, ASL does not do that, instead relying on the user themselves to calculate the game state. While ASL in theory could be used to make any application multiplayer, it favors certain types of applications over others and it is advised that you use it as intended - to create collarbative applications not based upon a physics movement system.</p>		
	</body>
</html>





