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

## Install Blender Pipeline Tools

## Set up the Pipeline

## Running Blender

## Set up Flamenco Rendering