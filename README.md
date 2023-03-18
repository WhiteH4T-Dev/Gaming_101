## Why Ubuntu?
Ubuntu is a great choice for gaming because of its stability, security, customizability, and support for a wide range of hardware. It is based on the highly stable and secure Debian Linux distribution, which means it is less likely to crash or experience performance issues while gaming. Additionally, Ubuntu offers a high degree of customizability, which makes it easy to optimize the system settings for gaming performance. Ubuntu also supports a wide range of hardware, including graphics cards from Nvidia and AMD, which makes it a versatile choice for gaming on a variety of systems. Overall, Ubuntu is a solid choice for gamers who want a stable and customizable operating system that offers good support for gaming hardware.

<br>

## How do I install Ubuntu?
- **Download Ubuntu ISO file:** First, you need to download the Ubuntu ISO file from the official website (https://ubuntu.com/download). Choose the appropriate version and architecture (32-bit or 64-bit) based on your system configuration.
- **Create a bootable USB drive:** After downloading the ISO file, you need to create a bootable USB drive. You can use tools like Rufus, Etcher, or UNetbootin to create a bootable USB drive.
- **Boot from the USB drive:** Once you have created the bootable USB drive, insert it into your computer and reboot the system. Make sure to select the USB drive as the primary boot device in the BIOS settings.
- **Choose installation options:** After booting from the USB drive, you will be presented with the Ubuntu installer. Choose the language and click "Install Ubuntu".
- **Configure network and updates:** On the next screen, you will be prompted to connect to a network and select whether to install updates during the installation process.
- **Choose installation type:** On the next screen, you will be prompted to choose the installation type. You can choose to install Ubuntu alongside an existing operating system, erase the disk and install Ubuntu, or choose manual partitioning.
- **Create user account:** After choosing the installation type, you will be prompted to create a user account. Enter your name, computer name, username, and password.
- **Wait for installation to complete:** Once you have configured all the settings, click "Install" and wait for the installation to complete. This may take some time depending on your system configuration.
- **Reboot the system:** After the installation is complete, you will be prompted to reboot the system. Remove the USB drive and reboot the system.

<br>

## What is Proton?
Proton is a software tool developed by Valve Corporation that enables users to run Windows applications and games on Linux operating systems through the Steam platform. It works as a compatibility layer, built on top of the popular Wine software, which translates the system calls made by Windows applications and games into native Linux commands. Proton is specifically designed for gaming, with features like improved support for DirectX 11 and 12, controller support, and automatic configuration of game settings. It allows users to play many popular Windows games on their Linux systems without the need for a virtual machine or dual-boot setup. Valve maintains a compatibility database on the Proton GitHub page that lists games that have been tested and verified to work with Proton, along with any known issues. While not all games are guaranteed to work perfectly with Proton, it has greatly expanded the library of games available on Linux systems and has helped to promote Linux as a viable gaming platform.

<br>

## Configure Ubuntu for Gaming
Download and install the latest updates for your system and installed applications
```
sudo apt-get update && sudo apt-get upgrade -y
```

<br>

Install Nvidia graphics drivers. These drivers are necessary to ensure optimal performance and compatibility with your graphics card.
```
sudo apt-get install nvidia-driver
```

<br>

Install a tool called neofetch to verify that your graphics card is being detected.
```
sudo apt-get install neofetch
```

<br>

Run neofetch and see if your graphics card is listed
```
neofetch
```

<br>

If your graphics card does not show remove the package you just installed
```
sudo apt-get purge nvidia-driver && sudo apt-get autoremove
```

<br>

Now try to run these commands below.
```
sudo add-apt-repository ppa:graphics-drivers/ppa -y
sudo apt update
sudo apt install nvidia-driver-495 libnvidia-gl-495 libnvidia-gl-495:i386 libvulkan1 libvulkan1:i386 -y
```

<br>

Moving on, now that you have your nvidia driver installed we will want to install a new kernel designed for gaming.
```
echo 'deb http://deb.xanmod.org releases main' | sudo tee /etc/apt/sources.list.d/xanmod-kernel.list && wget -qO - https://dl.xanmod.org/gpg.key | sudo apt-key add -
sudo apt update && sudo apt install linux-xanmod -y
sudo reboot
```

<br>

Now we will make a modification that will allow your system to compile faster
```
echo "RADV_PERFTEST=aco" >> /etc/environment
```

<br>

Now that your device is setup with the basics, now we can move onto installing Steam.
```
wget https://cdn.cloudflare.steamstatic.com/client/installer/steam.deb
chmod +x steam.deb
sudo dpkg -i steam.deb
sudo apt-get --fix-broken install
```

<br>

Steam will now be installed on your system. Open your menu and launch steam. Alternatively you can run steam from the terminal but it wont remember your login information.
```
steam &
```

<br>

When you are on the main screen of steam, look at the top bar of the app, click on steam then click on settings. Click on Steam Play. Make sure that the Enable Steam Play for Supported Titles and Enable Steam play for all other titles is checked and that you see Proton experimental as default. Click ok and quit steam. You might have an item in the top of your screen, right click and click on quit. It should however provide you an option to restart steam,if steam doesnt launch then run it from menu again.

<br>

Now that you have Steam installed and configured the next step would be to install a game. So in this example you will install Dying Light which is a Zombie Game. Once the game is finished installed quit steam fully. You will now need to install a custom version of proton on your system, this version has been developed by some devs that know their shit. Once steam is closed open a terminal and follow exactly what i say.
```
cd
mkdir ~/.steam/root/compatibilitytools.d
cd Downloads
wget https://github.com/GloriousEggroll/proton-ge-custom/releases/download/GE-Proton7-51-diablo_4_beta/GE-Proton7-51-diablo_4_beta.tar.gz
```

<br>

Keep the terminal open and open your file manager, right click and select extract. This will extract it. The next step will be to move this to the folder that was created. Follow the steps below.
```
chmod +x -R *
sudo mv GE-Proton7-51-diablo_4_beta ~/.steam/root/compatibilitytools.d
```

<br> 

This should have the folder that we extracted in the ~/.steam/root/compatibilitytools.d directory. You can now close the terminal and proceed with the last couple of steps. So once your game is installed on steam. Navigate to Library > select your game from the side menu, you will see a settings icon on your game, click on it and select settings. Set the steam launch options to the following.
```
-dxlevel 81 -sw -noborder -nofbo -nopreload -novblank -gl -glsl -glcore -glvbo -glshader -glpixel -glvertex -gladapter %GPU_ID%. 
```

<br>

Select the Compatibility tab and set the steam version to the new proton version we downloaded. you can close the window when you are done. Now all you have to do is launch the game, it will automatically go and download and configure your game. If it shows processing vulkna shaders dont press skip, its important. There you have it, gaming on linux with steam. 

