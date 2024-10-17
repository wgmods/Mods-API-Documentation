1. In WorldOfWarships/bin/[largest build number]/res_mods/, create a folder "PnFMods" and an empty text file "PnFModsLoader.py"

   ![image](https://github.com/user-attachments/assets/7ec15665-485f-474e-9614-e29a1853712a)

2. Take the latest ModsSDK_X.X.X.zip from https://github.com/WG-devacc/ModSDK
(Click on Download ZIP)

![image](https://github.com/user-attachments/assets/fbf43441-ef99-459b-8512-c764b5409f80)

Unzip the downloaded file, find the ModsSDK_X.X.X folder. Then, find the ID/name of the desired ship's folder and create a folder called "ModsSDK.zip" in PnFMods/, where you'll put the "[Ship_ID]" folder inside.

“Ship_ID” means the folder names in ModsSDK_X.X.X, i.e.

![image](https://github.com/user-attachments/assets/701f586f-cab7-43f6-b576-549702c9185c)

3. Create a Main.py file in PnFMods/ModsSDKExport/ with Python code:

API_VERSION = 'API_v1.0'

contentSdk.extractSources('[Your_Mod_Name]', '[Ship_ID]')

Example: If you want to make a mod called “Hashidate_Mod” for the ship Hashidate, you need to write this:

API_VERSION = 'API_v1.0'
contentSdk.extractSources('Hashidate_Mod', 'JSC037_Hashidate_1940')

4. Run the game client, wait for the extraction.

The game will get stuck at the logging screen. Use Task Manager to force the game to exit. (Keyboard shortcut: Ctrl+Shift+Esc) 

After extracting you will have the directory with  Your_Mod_Name in the PnFMods directory. Example for the Hashidate_Mod:

![image](https://github.com/user-attachments/assets/43c4eec2-5f5d-4474-8490-cdf461db4927)
