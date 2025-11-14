# Teagan's Capstone Artist Setup for Blender

## Install and Configure WireGuard VPN

The Bender pipeline for Teagan's Capstone Project is being hosted on her parent's home network.  In order to access that network, you need to install and run the WireGuard VPN client on your computer.

1. Install the WireGuard app by clicking the following link: <https://download.wireguard.com/windows-client/wireguard-installer.exe>.

   **_NOTE:_** Rather than download the file, you can choose to just run the program by choosing **Open** from the window that pops up when you click the link.  This way, you will not need to remember where the installer was downloaded to in order to run it and delete it later.  **Normally, this is a security risk that I do not encourage**.  However, since I have created these steps specifically for Teagan's team, I have vetted the process and trust it.  If you prefer to download the install program, make note of where you downloaded the file so that you can run it and then delete it when finished.  Open the folder where you downloaded the file installer and double click it to start the program.

1. Click **Yes** when asked, **Do you want to allow this app to make changes to your device?**

1. WireGuard should now be installed and you are presented with it's main window.

1. At this point, you need to reach out to me and I will send you a file that is unique to you.  Each of you have your own keys to access the VPN and I have a simple import file for you to use.

1. Click the button that says, **Import tunnel(s) from file**.

1. Navigate to the folder where you saved the config file I sent you and select the file and click **Open**.

1. At this point, the VPN should be ready to go and you should see an **Activate** button.  Click that button to activate the VPN.

   **_NOTE:_** The **Activate** button will change to **Deactivate** when the VPN is active/

1. If all has gone well, the VPN sould now be active.  Here are some ways to verify that the VPN is working properly.

   - you should see a successful handshake under the peer section of the WireGuard app.

   - There should be some data transferred showing in the peer section of the wireguard app.

   - Open a **Command Prompt** and type:  
   `ping -c3 mordecai.ankersen.dev` or  
   `ping -c3 rigby.ankersen.dev`.  
   You should see a response similar to: 
   **Reply from 192.168.20.24 time=5ms**.  If you see any other response, there is a connection issue and we will need to debug.

**_NOTE:_**  It is not necessary to keep the VPN running at all times.  You may deavtivate it when you are not working on the pipeline.  However, VPN is only used for accessing the pipeline serversand you really shouldn't even know it is there.  One downside to stopping the VPN is that the Flamenco Rendering Farm will not be able to use your computer as a part of the farm while you are disconnected.

## Install python

The Blender Studio Pipeline is heavily dependent on the Python programming language.  Python, and some specific Python modules need to be installed and configured on your local system.

1. Download the latest python release from: <https://www.python.org/downloads/windows/>

   **_NOTE:_** The Latest Python 3 Release is, as of 20 Sept, is 3.13.7

   **_NOTE:_** Just like the Wireguard install, rather than download the file, you can choose to just run the program by choosing **Open** from the window that pops up when you click the link.  This way, you will not need to remember where the installer was downloaded to in order to run it and delete it later.  **Normally, this is a security risk that I do not encourage**.  However, since I have created these steps specifically for Teagan's team, I have vetted the process and trust it.  If you prefer to download the install program, make note of where you downloaded the file so that you can run it and then delete it when finished.  Open the folder where you downloaded the file installer and double click it to start the program.

1. On the first page of the Python installer, there are two check boxes:  

   - Use admin priveledges when installing py.exe
   - Add python.exe to PATH

   be sure to check both of these before clicking **Install Now**.

   **_NOTE:_** There is no need to use the **Customize installation** option.

1. Click **Yes** when asked, **Do you want to allow this app to make changes to your device?**

1. After the installation completes, open a command prompt or terminal window and enter:  
`python --version`  
If the installation was successful, the Python version you installed should be printed in your command prompt or terminal window.

1. Verify that **pip** is installed by entering:  
`python -m ensurepip --upgrade`

1. Install the **requests** Python package for the current user:  
`python -m pip install --user requests`

## Set up the Pipeline

There is a python script that will set up the pipeline for the project.  It will ensure that everyone is using the same verion of blender and that all the appropriate extensions are installed.

### Create the project folders

1. Find the **Command Prompt** app in the Windows Start Menu.  This is easily done by starting to type the word Command in the start menu search bar.

   **_NOTE:_** If you happen to use be a **PowerShell** user, be sure to use the traditional command prompt for this particular section.  Bizaarrly, Microsoft does not include all of the commands needed in the PowerShell.

1. Right click on the **Command Prompt** app and choose **Run as administrator**.

1. Click **Yes** when asked, **Do you want to allow this app to make changes to your device?**

1. Execute the following commands in this terminal:

   ```c:```  
   ```mkdir c:\blender.pipeline```  
   ```cd c:\blender.pipeline```  
   ```mklink /D render \\skips.ankersen.dev\blender.render```  
   ```mkdir capstone```  
   ```cd capstone```  
   ```mklink /D shared \\skips.ankersen.dev\blender.shared```  
   ```mklink /D svn \\skips.ankersen.dev\blender.vcs```

1. Close this Administator Terminal.  It's generally not a good idea to leave an admin terminal open any longer than needed since it allows you to perform potentially damaging operations on your system.  Simply enter the command: ```exit```

### Setup Access to the shared file server

1. Ensure that your connection to the WireGuard VPN is active. (see above section on WireGuard)

1. Open another **Command Prompt** but this time it should just be a normal execution.  **Do not run as an administrator**.

1. Access the file share server with your unique username and password.

   ```net use \\skips.ankersen.dev /savecred```

   **_NOTE:_** You will be prompted to enter the user name and password.

1. To verify that you are connected to the file server, run the following commands:

   ```dir c:\blender.pipeline\capstone\shared```  
   ```dir c:\blender.pipeline\capstone\svn```  
   ```dir c:\blender.pipeline\render```

   Each of these dir commands will show the contents of the respective folder.  If you see **File Not Found** then you have not successfully conected to the file server.

1. You must be successfully connected to teh file server before moving to the next step.  Please reach out to me if you need assistance.

### Run the deployment_assistant.py script

1. Execute the following commands in the terminal:

   ```cd c:\blender.pipeline\capstone\svn\tools```  
   ```deployment_assistant.py```

   This script will run for some time and it will:

   - Create a new folder under capstone called Local.

   - The blender application and all its plugins are installed to Local.

   - You will eventually be prompted to provide your Kitsu login information.

   - Updates Blender with your Kitsu login information.

1. If all has gone according to plan, the script will finish and your Blender Pipeline is ready to use.

1. Close the Command Prompt, you are finished with it.  Simply enter the command: `exit`

## Running Blender

### Create a shortcut to the Capstone-Blender on your desktop

The blender studio tools allow an artist to have multiple copies of blender installed.  Basically, there is a unique version of blender for every project an artist is working on.  This allows for different versions and different plug-ins for projects.  It will also not interfere with a self installed version of blender on your system so there is no conflict if you already have blender installed.

However, because there are possibly multuple copies of blender in your system, you need a way to start the proper version for the project you are working on.  Fortunately, the pipline installs a helper script that will start the correct version of blender when you are working on the Capstone project.  All that is needed is to create a shortcut to that script on your desktop and then use it when you are woking on this project.  The easiest way to do that is via the Windows File Explorer.

1. Open your File Explorer

1. Click in the address bar at the top of the file explorer and enter: 

   ```C:\blender.pipeline\capstone\svn\tools```

1. Look for the file called: `launch_blender_win`

1. Right-Click on that file and hold while dragging the file to a spot on your desktop.

1. When you release the mouse button, a menu will appear.  Choose **Create shortcuts here** from that menu.

1. You should now have a new item on your desktop called **launch_blender_win - Shortcut**.  Let's give it a more descriptive name.

1. Right-Click on the new item and and slect **Rename** from the menu.

1. Call the item `Studio Teagan - Blender`, or any other descriptive name you prefer.

1. Once you have entered the new name, just hit the **Enter** key to confirm it.

## Set up Flamenco Rendering Farm
