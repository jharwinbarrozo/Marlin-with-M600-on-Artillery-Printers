Visit thingiverse https://www.thingiverse.com/thing:4251390 for most up to date changes!

Artillery Sidewinder TFT firmware G2 Beta v1.3.x. This is NOT an emulation, but true M600 with filament runout on the TFT and through Octoprint. This is a beta release, alpha release will be 1.4.0 and will be the designation once it is established that everything is running smoothly. Let me know if you find any bugs. And check back for newer versions if you have a bug, I repair them quickly.

I don't get paid for this, so please support my YouTube channel!

M600 feature video about how I pulled it off:
https://www.youtube.com/watch?v=HJpfO8XifqI&t

Installation and Setup Guide with a brief walk through of features:
https://youtu.be/Fp-cJR8ta9s

Discord for up to date bugfix and feature discussions:
https://discord.gg/jDvYhaN

1.3.22 and later Install Instructions:

Prior to installation, make sure the correct USB drivers are installed (CH340, included in the download). If Windows does not automatically find the correct driver, the included files go into the "windows\system 32" folder. Then update the driver of the com port associated with the printer under the Ports category of your Device Manager.

STEP 1: Unzip package and run Marlin-ArtilleryX1_2.0_Devel\Marlin\Marlin.ino . You may need to download Arduino IDE for this step (
https://www.arduino.cc/en/main/software
).

You should make sure the correct board is configured in the Tools menu: Board: "Arduino Mega or Mega 2560", Processor: "ATmega2560 (Mega2560)", Programmer: "AVRISP mkII", Port: {select your COM port here}.

You may instead use Visual Studio Code if you are comfortable with that process.

STEP 2: Look for the Artillery Options header around line 42 of Configuration.h. Below you will see options for defining automatic bed leveling, Nozzle To Probe Offset, the BMG extruder, Nova hotend, 104gt2/Hisens 3950 thermistor, whether or not you have a Genius, or whether to use S Curve Acceleration. Comment/uncomment out accordingly (lines beginning with // are commented out and will be disabled).

STEP 3: Make sure USB is disconnected and Compile Marlin (Checkmark Icon at the top).

STEP 4: While Marlin is compiling, open the printer case and disconnect the two-wire red/black RESET cable between the TFT and mainboard. Once this is disconnected you will no longer need to open the printer to flash. Leave the gray 4-wire ribbon cable attached.

NOTE: For Older Sidewinder X1 (V1-V3) without the reset button, ignore this step and follow the remaining steps precisely. Do NOT unplug the TFT ribbon cable during flashing.

STEP 5: Move the filament runout sensor (cable with three white wires) from PB1 on the TFT to the X max endstop aka D2 (orange connector labeled X+) on the mainboard. It aligns correctly with the shape of the connector in the same direction as the X, Y, and Z endstop connectors next to It. You may have to remove some hot glue to get the connector seated. Genius users may have to extend the wires to the runout sensor!
If you are using BL Touch, upon uncommenting BLTOUCH it will be defaulted to the same wiring configuration as Waggster Mod. You may also comment out WAGGSTER_MOD_WIRING to use the Z- connector - where the factory Z endstop was connected. This is an option in the Artillery Options section of Configuration.h. You may now fully reassemble the printer.

STEP 6: Unzip mkstft28.bin and the bmp and font folders from mkstft28_g2_v1.3.xx.zip directly to an SD card, put it in the printer and RESTART.

STEP 7: Go to Menu->Settings->FLASH FW. The screen will say "You can now FLASH Marlin."

STEP 8: Plug in USB and click Upload in Marlin ("->" Right Arrow Icon at the top). MAKE SURE YOU HAVE DISCONNECTED THE RED/BLACK WIRES FROM THE TFT BEFORE TRYING TO FLASH! If you have issues uploading, sometimes unplugging the USB cable and reconnecting it resolves connection issues.

STEP 9: Touch the screen to exit the Disconnect menu and click "Confirm" to automatically load default firmware settings with M502 and save with M500.

STEP 10: Go to Menu>Settings>Features and toggle the features for your particular setup: Sidewinder/Genius ABL/Manual Mesh, 285 MAX/375 MAX hotend temperatures.

STEP 11: PID Tune the Hotend and the Bed. A dialog should prompt you to do a full PID tune of the hotend and bed the next time you load the Status screen. If it does not appear, or you ignore the dialog, you can navigate to the Custom Gcode menu and run both PIDTUNE H and PIDTUNE B at any time. Failure to PID tune before printing may cause "Printer halted. kill() called!" errors upon heating.

You’re done!

NOTE: You do not have to include the "bmp" and "font" folders every time you update the TFT firmware, only when the ICONS are mentioned as being changed. You do not have to update Marlin every time you update the TFT firmware, only when MARLIN is mentioned as being changed.
*USB DRIVE PRINTING IS DOWN FOR VERSION 1.3.38. It will be fixed within a day or so.

A few things to look out for:
The motor steps are adjustable through the TFT but the process is very annoying right now. It will be fixed soon.
A recent connection bug was addresses. Let me know if you get any Unknown Command errors or the print seems to skip the start g code and cold extrude.

1.3.38 G2: Strange connection bug addressed by adding a 1ms delay between commands. Other minor improvements. CHANGES TO: TFT. NO CHANGES TO: ICONS, MARLIN.

1.3.37 G2: This should stabilize the temperature readings, and revert to using M109 and M190, while implementing a new algorithm to detect the end of a heating busy state. CHANGES TO: TFT. NO CHANGES TO: ICONS, MARLIN.

1.3.36 Updates include new dialogs for Home XY first and Home Z first, M600 is now used for pausing instead of M0 so the nozzle will park, all new sounds (yes, plural) and buzzer handler which should fix the buzzer problem. We can play around with the sounds. I recently broke the parameter menu and have brought it up to speed with recent changes. Lots of backend cleanup and preparation for future features, some miscellaneous bugfixes. CHANGES TO: TFT. NO CHANGES TO: ICONS, MARLIN.

1.3.35 G2: Minor connection protocol updates. Switching between Manual Mesh and ABL should be automatic now. Baystepping and Z offset should be working with ABL setups now. There have been alot of changed on the backed as the transition is made to a more efficient way to track parameter values, so 1.3.34 is still available for now. The previously unused parameter_settings.bmp was missing from the unified icon set, and is provided here. CHANGES TO: TFT, ICONS. NO CHANGES TO: MARLIN.

1.3.34 G2: JD_HANDLE_SMALL_SEGMENTS has been disabled in Marlin due to this known bug:
https://www.gitmemory.com/issue/MarlinFirmware/Marlin/17342/645493437
. Babystepping has been repaired for Manual Mesh mode. I will be checking on ABL babystepping and Z offset menu operation today. CHANGES TO: TFT, MARLIN. NO CHANGES TO: ICONS.

1.3.33 G2: I was finally able to run a few tests on the new Z offset method and I was not working for MBL. I have not tested on ABL yet. The configuration problems with Marlin should be fixed now, and with all the progmem cleared up in the debugging process we are now running S_CURVE_ACCELERATION! ENDSTOP_INTERRUPTS_FEATURE was causing hesitation and strange sounds. We are commited to InsanityAutomation branch of Marlin for the foreseeable future. CHANGES TO: TFT, MARLIN. NO CHANGES TO: ICONS.

1.3.32 G2: Compatibility with older Sidewinder versions was not fully implemented, this corrects that. Marlin configuration errors also corrected. Work to resolve some Marlin performance issues is ongoing. Also included is an alternative version of Marlin 2.0.5.3 from before the recent bugfix/InsanityAutomation merge. It is temporarily provided for troubleshooting purposes. A decision will be made soon about which branch will become primary. CHANGES TO: TFT, MARLIN. NO CHANGES TO: ICONS.

1.3.31 G2: Bugfix for serial communication with Marlin. CHANGES TO: TFT, MARLIN. NO CHANGES TO: ICONS.

1.3.30 G2: New Icon Set Option! Select the set of your choice and put that "bmp" folder on the SD card and reboot to install them. This can be done wth or without flashing the TFT firmware. 1.3.30 TFT firmware has experimental and untested upgrades to the babystepping and Z offset menu that will reference the Z offset value saved in Marlin instead of a relative position that starts at zero every time the machine is rebooted. This should be more intuitive. I have not tested the code, so 1.3.29 has been left available. In Marlin, square wave stepping has been disabled. CHANGES TO: TFT, ICONS, MARLIN.

1.3.29 G2: Another hack at the buzzer issue. If it gets stuck on for you, go to Menu>Settings>Screen and Toggle Silent (After a few days with no complaints, I am tempted to call the issue fixed). Titles now added to parameter menu so you can tell what axis you are editing. Substantial code was added to parse parameter values from M503 commands and populate the Marlin configuration in the TFT, though only minor use was made of them on this release. The parameter for TMC motor current has an indicator as to whether or not the parameter is enable in Marlin (red=not enabled, green enabled). CHANGES TO: TFT. NO CHANGES TO: ICONS, MARLIN.

1.3.28 G2: Another attempt at fixing the USB printing error. This new approach shows promise. An attempt was made to handle the beep getting stuck on. Enhancements to serial communication stability. CHANGES TO: TFT, MARLIN. NO CHANGES TO: ICONS.

1.3.27 G2: Due to variable G0 being used in the TFT firmware, the following change was reversed from the recent stuttering debug session: configuration_adv.h #define VARIABLE_G0_FEEDRATE. Also "too cold extrusion" handling has been added that will prompt you with the option to preheat to PLA when a cold extrusion event occurs, as well as upping the extrude menu distances from 1,5,10 to 1,10,50. Improved filament runout control, now integrated with toggle in feature menu (untested).

1.3.26 G2: USB drive functionality should be fixed {it was not}! As well as full functionality for V3 and older Sidewinders. Autosave is now enabled for parameters. Other minor tweaks.

1.3.25 Improved connection reliability again. Marlin configuration was revised to solve stuttering problem. USB stick printing is still not fixed!

1.3.24 G2: An attempt to add reverse compatibility to Sidewinder versions older than X1 V4 has been made. Compatibility with all printers is untested beyond loading the TFT SD card volume to the screen. 1.3.24 will probably have multiple revisions. V4 and Genius users should not bother with this version as it is untested and adds nothing new for you.Testers are, of course, appreciated. Also in testing this version is an update to the 6/17-2020 release of Marlin via the InsanityAutomation Branch. Previous versions were not updated to his branch specifics. This new configuration has been spliced with his to support for skr13 and tmc2209 (untested). Increased connection reliability between TFT and Marlin.

1.3.23 G2: More tinkering. This is a placeholder version. This is the first time I've had a chance to print anything in awhile and this one seems to be running well so far. I'm hoping this is stable enough that I can focus on other projects this week.
*Z min sensor as probe configuration is getting some love and a patch has been applied to 1.3.23. A tester should report back soon so that 1.3.24 will be tested working for that configuration. UPDATE: ZMIN_SENSOR_AS_PROBE seems to be working!

1.3.22 G2: Improved connection stability to Marlin upon disconnect and Octoprint connect events.

1.3.21 G2: 1.3.20 was a debug version and the TFT would not properly connect to Marlin under most circumstances. It was accidentally released. This is a correction.

1.3.20 G2: Minor optimization to connection protocols. Quieter operation on the serial port.

1.3.19 G2: PID tuning added to the installation instructions, and to the Feature menu. A dialog will now prompt for full PID tuning after leaving the disconnect menu, initializing new firmware, and returning to the Status Screen. Lots of Nova configuration work. TMC motor current is reenabled in the Parameters menu. Some backend Optimization and improvement.

1.3.18 G2: "wait" is no longer displayed in the terminal. For versions 1.3.15-1.3.17 there was only 1 Z stepper defined due to the transition to the new branch of bugfix Marlin. This has been corrected. 3dprintbeginner Z_MIN sensor as ABL probe has been added to Artillery Options.

1.3.17 G2: Changed default move distance from 1mm to 10mm in the Move menu. Modified the autoreport XYZ positions to occur on their own line for better parsing fof temperatures by Octoprint.

1.3.16 G2: Renovated the dialog handling code to clean it up. It may run better. Clicking on the gantry XYZ positions from the status screen now brings you directly to the Unified Move menu and the gantry XYZ display area is larger.

1.3.15 G2: Better dialog handling. Minor visual glitch repair. Compatibility for TFT35 added back into source code (untested, and the changes for this are the reason for a few recent visual glitches). New version of Marlin:
SHORT_BUILD_VERSION "bugfix-2.0.x"
STRING_DISTRIBUTION_DATE "2019-07-10"
https://github.com/InsanityAutomation/Marlin/tree/ArtilleryX1_2.0_Devel

This new version of Marlin was capable of running the M600 dialogs without backend modification! I did modify the function of M155 to also send XYZ positions though. Testing with this version is very limited, so 1.3.14 will remain available with 2.0.5.3 until this new version is established as a viable replacement.

1.3.14 G2: versions 1.3.12 and 1.3.13 had a bug that would not update the fonts and icons from the folder specified in the installation instructions. This would not affect you if you were upgrading from one version to another, it only affected fresh installs. This version is a minor fix for the definition of ROOTDIR on the SD card.

1.3.13 G2: Added speed/flow/fan display and easy access to the printing menu. Minor bugfix for visual glitch where a small portion of a button would not be cleared after leaving the print from source menu. I'm thinking about rescaling the icons and optimizing the screen layout.

1.3.12 G2: more Zoffset Menu repair for non-ABL users. Babystepping and easier access to temperature and flow settings is enabled during Octoprint sessions. The Marlin FLASH procedure has been greatly simplified due to a greater understanding of the process and no longer requires RESET of any kind. Waggster Mod BL Touch wiring is now the default configuration in Artillery Options of Configuration.h. Other minor bug fixes. M600 dialogs now automatically disappear when they are handled by Octoprint instead.

1.3.11 G2: .gco files now supported in addition to .gcode. Legacy Marlin Mode automatically enabled in the event of an Unknown Command for M155 or M75, which reverts to use of M105 and M114 commands (untested). Hemera option added to configuration.h header (untested). 104gt2 Thermistor also added to header section.

1.3.10 G2: Full M600 functionality! Marlin 2.0.5.3 is now configured and included in the download. Artillery Options section at the top of Configuration.h to ease compatibility with various platforms - list will grow. Genius compatibility added. Manual Mesh added. See Menu->Settings->Feature menu for toggle between those modes. External Host Active mode to silence all TFT commands during Octoprint sessions. M155 is used instead of M105. M155 has been modified to poll M114 positions along with temperatures ('P' parameter). This was done to better display the layer height during Octoprint sessions. A recently developed bug in updating the temperatures o the status screen was resolved. Z Offset feature completely rewritten, and is now live Z offset. Babystep feature now autosaves. Feature menu selection toggle for Nova hotend. Bug that would allow freezing the display on previous version has been resolved. 50mm move option now added to the move menu (0.12mm, 1mm, 10mm, 50mm). XYZ Position and Temperature always displayed. Motor Steps/mm are now adjustable through the parameters menus. Other minor menu reordering and improved functionality.
Others: Special thanks to Doron, and Gavin of team Fulament, and Ryan for help with testing and configuring Marlin for Manual Mesh and the awesome brainstorming toward getting M600 working!

1.3.9 G2: menu reordering for better workflow. Added always displayed XYZ positions. Completely recoded the Z offset feature that was apparently started and abandoned in the original source code. Added a 50mm move distance to the move menus.

1.3.8 G2: Temperatures are now displayed at all times (with the exception of a few menus). Parameters menu has been added, which has provisions for setting esteps and other axis steps/mm. Z offset did not work previously. In this version the z position moves to 0 at the center of the bed so you can correctly get the z offset, and the motors move now so you can see what you are doing. Values will automatically save when you exit the menu. Future versions may simplify the process to exclude the preliminary movement - this has not been decided. The parameter for the motor current are completely disabled and will likely be removed on the next version, as it it very hard to click the correct axis when setting steps with such a small screen. Movements that were previously 10mm are now 20mm, though the icons and labels have not been updated to reflect this yet (sorry!).

1.3.7 G2: Fixed the disconnect feature! The source code will not been updated beginning from this point.

1.3.6 Ozollo: Deleted uneccesary files from source code and made a few revisions to clean up the code that will not affect performance. G2: Beep added to print completion. List mode enabled on file menu to read long file names. ABL added to "Home" menu. Attempted bug fix for potential menu hangup - success unknown as of this time.

1.3.5 Ozollo has joined the project and fixed his first bug: M500 added for PID autotune. Prior to version 1.3.5 the PID autotune features in the Custom menu did not autosave.

1.3.4 Prior to version 1.3.4, there was a bug in the cancel print function that would throw a Halt! Printer Stopped error. cancel_print_gcode modified.

1.3.3 Prior to version 1.3.3, the icons were designated to the wrong folder for uploading, so if you weren't already using the unified icon set you would have garbled icons.

1.3.2 Prior to version 1.3.2 there was a bug that would crash the extruder into a print taller than 50mm at the end code. I caught it almost immediately, but this was available for a few hours, so if you were one of the first to download, you'll definitely want to get a newer version.

Features:
M600 is fully enabled and the filament runout sensor works on both Octoprint and the TFT.
This version is configured for the build volume of the Sidewinder or the Genius.
By request, Manual Mesh has been added.
Preconfigured Marlin is now included.
Support for the BMG extruder and Nova Hotend have been added.
Motor Steps are accessible through the TFT.
PID tuning is incorporated for both the bed and extruder with autosave.
Live flow/speed/temperature adjust and babystepping.
Filament runout sensor is enabled!
GCode console interface (accessed by touching the "Info" box on the main status screen or looking for the GCode menu).
It is enabled for both manual leveling and BL Touch (if you have that enabled in your Marlin firmware).
The center leveling point has been added, and the corner leveling points are positioned above the mounting points instead of at the far corners.
There is a disconnect feature so you can flash without unplugging the TFT cable.
Custom GCode is added to raise the z axis by 100, lower the z axis to 10, present bed to position Y250 for part bed cleaning/part removal, and extrude 100mm of filament.
Some of the menus are made more circular so it is easier to get between preheating, moving, and extruding.
There are presets to preheat PLA, ABS, PETG, with option to toggle the bed/nozzle/both as well as a quick button to preheat the bed to 65.
Magic numbers are hard coded into all touchscreen axis moves (0.12 and 0.04mm instead of 0.10 and 0.01 respectively). The max denomination of manual axis movement is 50mm.
Percentage progress bar and z axis position are displayed during print.
The bed presents itself to position Y220 upon canceling of the print for bed cleaning/part removal.
Beep upon print completion.
Display and editing of Esteps and XYZ steps and TMC motor voltages.

Future features goals include:
display of M503 parameters,
graphic display of bed leveling data,
scrolling for long file names,
mkstft.txt configuration support,
Linear Advance K, PID values, acceleration and other parameters will be added to the TFT menus.

If you have any problems or suggestions, or if you want to help make new icons, let me know.

Also included is v3 of a lightweight ribbon cable support for use with an extra 10 conductor rainbow ribbon cable. Original bolts and a zip tie are all that is needed. I also posted it separately, but Thingiverse wanted an stl file so you get it here...

You can find the source code up to v1.3.6 here:
https://github.com/G2Barbour/MKSTFT28_Clone_Artillery-Sidewinder

The github will no longer be updated.

This is adapted from one of the many BigTreeTech msktft28 TFT firmware variants out there. The origination of this code is the mkstft28_v1.0 Clone version made for the Genius by Darkspr1te/Blueforcer. You can find it here:
https://codeload.github.com/Blueforcer/MKSTFT_Marlin_Touch/zip/0.0.2

New Icon Source:
https://github.com/bigtreetech/BIGTREETECH-TouchScreenFirmware/issues/428
