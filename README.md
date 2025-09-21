# Teagan's Capstone Artist Setup for Blender

## Install and Configure WireGuard VPN

The Bender pipeline for Teagan's Capstone Project is being hosted on her parent's home network.  In order to access that network, you need to install and run the WireGuard VPN client on your computer.

1. Install the WireGuard app by clicking the following link: <https://download.wireguard.com/windows-client/wireguard-installer.exe>.

   **_NOTE:_** Rather than download the file, you can choose to just run the program by choosing **Open** from the window that pops up when you click the link.  In this case, you will not need to remember where the installer was downloaded to in order to run it and delete it later.  Normally, this is a security risk that I do not encourage.  However, since I have created these steps specifically for Teagan's team, I have vetted the process and trust it.

   **_NOTE 2:_** If you prefer to download the install program, make note of where you downloaded the file so that you can run it and then delete it when finished.  Open the folder where you downloaded the file installer and double click it to start the program.

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
   `ping mordecai.lab.ankersen.dev`  
   You should see a response similar to:  
   `Reply from 192.168.20.24 time=5ms`  
   If you see any other response, there is a connection issue and we will need to debug.

**_NOTE:_**  It is not necessary to keep the VPN running at all times.  You may deavtivate it when you are not working on the pipeline.  However, VPN is only used for accessing the pipeline serversand you really shouldn't even know it is there.  One downside to stopping the VPN is that the Flamenco Rendering Farm will not be able to use your computer as a part of the farm while you are disconnected.

## Install python

The Blender Studio Pipeline is heavily dependent on the Python programming language.  Python, and some specific Python modules need to be installed and configured on your local system.

1. Download the latest python release from: <https://www.python.org/downloads/windows/>

   **_NOTE:_** The Latest Python 3 Release is, as of 20 Sept, is 3.13.7

1. On the first page of the installer, ensure the option labeled “Add Python to PATH” is enabled.

1. After installation completes, open a command prompt or terminal window and enter: `python --version`.  If the installation was successful, the Python version you installed should be printed in your command prompt or terminal window.

## Set up the Pipeline

There is a python script that will set up the pipeline for the project.  It will ensure that everyone is using the same verion of blender and that all the appropriate extensions are installed.

1. Open a windows command prompt and execute the following commands.

   ```bat
   mkdir c:\blender_pipeline
   cd c:\blender_pipeline
   mkdir capstone
   mkdir capstone\shared
   mkdir capstone\svn
   mkdir flamenco
   ```

1. Run the **deployment_assistant.py** script.

   ```bat
   cd capstone\svn
   deployment_assistant.py
   ```

## Running Blender

## Set up Flamenco Rendering
