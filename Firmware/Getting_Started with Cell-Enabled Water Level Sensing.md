# Getting Started with Cell-Enabled Water Level Sensing
## Particle and Visual Studio
This section will help you set up Visual Studio Code and Particle Workbench, two important platforms you'll need for the following exercises.

1. Download Visual Studio (the one with the blue icon, not purple) [here](https://code.visualstudio.com/).
2. Download Particle Workbench [here](https://www.particle.io/workbench/) and create an account using your email address of choice (select 'Education' for account type if applicable). Make sure you have Visual Studio installed prior to running the installer.
	- The installer says that it will install Visual Studio (VS) along with Particle, but this does not work properly and will fail if VS is not installed first.
3. Log into Particle on Visual Studio if it doesn’t automatically (this is important because you won’t be able to install necessary libraries without being logged in).

## Useful features
This section lists some commands and programming features that will be helpful in the following exercises.

1. Open the Particle Command Palette: Ctrl+Shift+P on Windows; or Command+Shift+P on Mac; or select the 'view' tab -> Command Palette; or click the 'Launch Command Palette' button on the 'welcome' tab).
2. In the top right corner, there are some important symbols in white circles:
	- Compile: checkmark
	- Flash: lightning bolt
3. These symbols will be used later to compile and flash code (i.e. importing code to the Boron device).
4. Save your projects frequently using Ctrl+S on Windows or Command+S on Mac. Make sure your directories are exactly how you want them to avoid pathway issues in your coding projects!
5. Keep this in your back pocket, but don't use it yet: in cases where the Boron stops responding as expected or displaying error LED sequences, you may need to restore the device. Particle has an online, USB-based option here: [https://docs.particle.io/tools/device-restore/device-restore-usb/](https://docs.particle.io/tools/device-restore/device-restore-usb/).

## Common problems
This section lists some common problems you may encounter in the following exercises and how to address them.

Skip this section for now and try the **Practice Code with Boron** section first. Refer back to this list if you encounter problems.
1. If you receive a "No Device Found" or "Serial Time Out" message when using "Particle: Identify" ... First, double-check that you have selected Boron in the bottom right bar, have selected the correct OS version (for me, it is 4.2.0), and put the device in listening mode (by pressing and holding the Mode button until the LED blinks blue). If those settings are correct but you're still having issues, try unplugging/replugging the device or restarting VS and/or your computer.
2. If you have problems in **Practice code with Boron and Adalogger** ... If Initializing SD Card and initialization failed, check that the micro SD card is empty. Plug it into your computer, open the SD card, and delete every file on it.
3. If met with unsuccessful compiling and a message stating that your file is dirty, try accepting the offer to 'clean' your file. If this doesn't fix the issue, try closing VS, deleting the project from your computer, and starting over.

## Practice water level sensor full code (Boron and Adalogger) 
This section will allow you to practice using water level sensor code and working with the Boron and Adalogger devices.

1. For ease of acces when flashing code to the Boron, we recommend taking the entire printed circuit board out of the SK-15 enclosure. Unscrew the four screws surronding the circuit and take it out of the enclosure. The power cord doesn't need to be plugged in as the micro USB connection from your computer will provide enough power. If possible keep the ultra rangfinder sensor plugged into the printed circuit board. Once you have the printed circuit board out (with Boron, addalonger... connected to it), procced to plug in micro-USB cable from your computer to the Boron.
2. 1. Plug in the Boron device to your computer using a micro-USB cable. Visit [https://docs.particle.io/tools/device-restore/device-restore-usb/](https://docs.particle.io/tools/device-restore/device-restore-usb/) and click 'Select Device.' Restore to the default system firmware version matching the example (not 'custom user firmware') and set the current compiled [target](SLR_Boron_Maxbotix_MB7092_cm/target) to be 6.1.0 (this is the version I am using).
	- Note: If you get the message `Could not identify device: No serial port identified` but the Boron powers up, ensure that your cable has data transfer capabilities (many are only capable of charging). Or, if no device is found using the device restore page, Put the Boron into DFU (Device Firmware Update) mode by pressing and holding the 'Mode' button on the Boron while simultaneously pressing and releasing the 'Reset' button.
3. Create a folder on your computer to store Particle-related items (no spaces in the title; use underscores (_) ... something like Particle_Items).
4. Create a new project by opening the Particle Command Palette (see: 'Useful features') and selecting 'Particle: Create New Project.' You can also click the blue text that says 'Create New Project' on the welcome page under Development Workflow -> Code.
5. Choose the folder you just made on your computer for this class when asked to choose the 'parent' folder.
6. Once you have the directory in which you want to store your Particle projects, create a project name (no spaces) ... something like Water_Level_Boron

7. On this GitHub repository, go to 'Firmware' -> 'SLR_Boron_Maxbotix_MB7092_cm' -> 'src' -> 'SLR_Boron_Maxbotix_MB7092_cm.cpp' (or follow [this link](https://github.com/COAST-Lab/Open-Water-Level/blob/main/Firmware/SLR_Boron_Maxbotix_MB7092_cm/src/SLR_Boron_Maxbotix_MB7092_cm.cpp)).
8. Copy all the code on this page after line 13 (i.e. lines 14 onward).
9. In Particle Workbench, create a new project (I named mine BAdaFull).
	- See 'Useful features' and 'Practice code with Boron' if you need a refresher on how to create a new project.
	- Optionally, you can fill in the header with your info (i.e. project, your name, date)

10. Open the Command Palette and type 'Particle: Install Library' 
11. Type in 'SdFat' and press enter to install the SdFat library.
12. Go to the .cpp file in the new project you created (it should have the same name as your project).
13. Delete all code after line 9 (i.e. lines 10 onward) and paste the new code you copied from GitHub (remember: must have `#include "Particle.h"`). Your new header should look like this:

<img src="Photos/BAdaFull_Header.jpeg" width="400">

14. In line 45, make sure the number after `#define PUBLISHING` is `0`.
	- If it says `1`, change it to `0`
 	- This step is crucial! It ensures that we aren't publishing data via cellular connection, which is important since we are just completing a test run.
	- Once a device is deployed with the intent of publishing data and using a cell connection, this binary value can be changed back to `1` ... but we aren't quite there yet, so make sure it says `0`!

15. At this point, I like to compile my code as a sort of "checkpoint" to make sure there aren't any issues. Click the check mark to compile.
	- If met with errors, make sure you have "Boron" and "4.2.0" selected in the page's bottom ribbon, and check that you completed each step of these instructions correctly.

16. Once your code compiles properly, flash it to the Boron by clicking the lightnight bolt. 
	- If your device is not responding or the flash is unsuccessful, make sure the device is in DFU mode, or try unplugging/replugging the cord.

17. Once flashed successfully, quickly open the serial monitor: Command Palette -> 'Particle: Serial Monitor'
18. It may take a moment, but the terminal should look something like the picture below. The serial monitor should say `serial connection closed. Attempting to reconnect…`

<img src="Photos/BAdaFull_SerialMonitor.jpeg" width="400">

If it still doesn't work, try the problem-solving methods from Step 16 again or visit 'Useful features' and 'Common problems.'

19. The numbers produced under `Serial monitor opened successfully:` represent four useful data values, listed as follows: Unix timestamp, distance measured by the sensor (cm), battery voltage (volts), battery level (%)
	- Lines 135-139 (pictured) show how these values are printed from the code.
	- Please note that Unix timestamps represent seconds since 1 Jan 1970. However, the Unix timestamps from our non-cellular trials represent seconds from 1 Jan 2000 each time the Boron is restarted. Once we use cellular connection when deploying the device, we'll have real time stamps (i.e. since 1970).
	- Please note that the battery voltage and battery level may show values of zero; these measures are related to an external rechargeable battery that we did not connect for these test trials ... Instead, we powered the device from a laptop / computer.

<img src="Photos/BAdaFull_Lines_135-139.jpeg" width="500">

20. To finish collecting data, unplug the Boron to stop the code from running.
	- Don't forget to save your project.
	- If you wish to run this test trial again and recieve data results in faster time intervals, you can change the `SECONDS_BETWEEN_MEASUREMENTS` value in line 74 from `3600` to `30`. This will take readings at 30 second intervals instead of hourly intervals. Just be sure to change this value back to `3600` when you officially deploy the device!

21. To check all the collected values, take out the SD card from the Adalogger and put it into an SD card reader to then plug into your computer.
22. Navigate to 'file explorer' -> 'this PC' -> 'USB drive' -> `distance.csv`. You should see a table with values like below!
	- On Mac, access this file via Finder -> Locations (Untitled) -> `distance.csv`

<img src="Photos/BAdaFull_csv.jpeg" width="300">

23. Unix timestamps are listed in the leftmost column, then distance (cm), then battery voltage (volts), and battery level (%) in the rightmost column.
	- If you want to save the data from the micro SD card, press ctrl+s (Windows) or command+s (Mac) to save the data file on your computer.

All done! Now, you're more familiar with powerful tools like the Boron and Adalogger devices and VS Code, and you've learned how to collect and store the distance data. Great work!
