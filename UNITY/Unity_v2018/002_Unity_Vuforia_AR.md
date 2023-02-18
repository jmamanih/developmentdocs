# Creat App AR for Android

##Vuforia AR

* Create marker images .jpg width Photoshop 
* [Open Vuforia Developer Page](https://developer.vuforia.com/)
* Register in Vuforia
* Login Vuforia
* Click Develop Option Menu, Target Manager, Add Database Button
	Create Database
		Name: database_name
		Type: Device
	Button Create
* Click database_name, click Add Target
	Type: Single Image
	File: Select image file format JPG
	Widht: 200
	Name: image_name

* Target Manager, Select Database_name, Click Dowload Database, Select a development plataform: Unity Editor, Button Download
* Create Licence Key 
	Open [Vuforia development portal](https://developer.vuforia.com/targetmanager/licenseManager/summaryForFreePlan), Licence Manager, 
	Add a Free Developmen Licence Key, App Name: nameApp, Button Confirm, click nameApp, copy Licence Key

## Unity

* [Download Unity](https://store.unity.com/es)
* Install Unity free (Personal)
* Create Unity ID [Register](https://unity3d.com/es/)
* Open Unity, autenticate
* Activate Personal License 
* Create Unity Project 3D
	Project name: nameApp
* Select Main Camera, right click, delete
* Download Vuforia SDK for Unity
	Open [Vuforia SDK](https://developer.vuforia.com/downloads/sdk) 
	Select Unity Extension (vuforia_unity_6.2.10.unitypackage)
* Section Assets, right clic, Import Package, Custom Package, select file vuforia_unity_6.2.10.unitypackage, All Button, Import Button
* Import Package select file vuforia_database.unitypackage
* Select Assets, Vuforia, Prefabs, Drag and drop AR Camera to Hierarchy Panel and Drag and Drop Image Target
* Select AR Camera, Righ Tab Inspector, Vuforia Behaviur (Script), Open Vuforia Engine Configuration

	Enabling Vuforia in Unity, follow these instructions to enable Vuforia in Unity 2017.2 or later.

    Open Unity 
    In the Edit Menu select: Project Settings > Player. In the “XR Settings” section of the PlayerSettings, make sure that “Vuforia Augmented Reality Supported” is checked.

* In Vuforia, App License Key: Paste License Key generated from Vuforia
* In Datasets, Check Load AR Database, Check Activate 

* Select ImageTarget, Right Tab Inspector select Image Target Behaviour (Script), select Database, select Image Target

* Select AR Camera, Camera set values Transform:
	Position: -12,  270, -392
	Rotation: 36.119, -0.534, -0.271
	Scale:    1, 1, 1
* Search [model 3d unity](https://www.assetstore.unity3d.com/en/)
	Select 3d Model Animated
	Click Open in Unity
	Unity Tab Assets Store, Download
* Select in Assets Section Model 3D downloaded, Drag and Drop to Target Image, adjust size model 3d to context




Download Unity Assistant for Elementas export Android, iOSx, etc
https://store.unity.com


### Export App to Android

* File menu, build settings, Add Open Scenes
	Platform: Select Android
	Player Settings:
		Company Name: La Paz Digital
		Product Name: ARNewsApp
		*Resolution And Presentation*
			Default Orientation: Landscape right
		*Other Settings*
			Identification
			Package Name: com.lapazdigital.arnewsapp
		Button Build
		Note: Android Studio SDK must be installed

Build errors:
=============
[1]
Error:Invalid command android
CommandInvokationFailure: Unable to list target platforms. Please make sure the android sdk path is correct.
[Solution]

Download Android Tools r25.2.5
for Windows
https://dl.google.com/android/repository/tools_r25.2.5-macosx.zip
for MacOSX
https://dl.google.com/android/repository/tools_r25.2.5-windows.zip

Got to SDK folder installed, rename folder tools, unzip tools_r25.2.5-windows.zip


Update Unity 3D 2017
https://unity3d.com/es/unity


