# Pubbly SchoolHouse

Cordova project for Swahili and English APK submissions.

## Structure

Original, the structure of the School House cordova project was to be determined from the Console itself. Each school was to have a grid based system, and each subject was to exist at a certain point in the grid. However, as the deadline approached, too many small changes were required, and so the application was half automated and half manually tweaked.

### App setup

First, install cordova. [Installing cordova](https://cordova.apache.org/docs/en/latest/guide/cli/#installing-the-cordova-cli)

Then create a new cordova project. 

* cordova create schoolHouse com.cci.schoolHouse SchoolHouse
* cd schoolHouse

Add android. [How to add a platform](https://cordova.apache.org/docs/en/latest/guide/cli/#add-platforms)

* cordova platform add android

And the following plugins. [Adding cordova plugins](https://cordova.apache.org/docs/en/3.0.0/guide/cli/index.html#add-features)

* cordova-plugin-autostart
* cordova-plugin-battery-status
* cordova-plugin-camera
* cordova-plugin-compat
* cordova-plugin-device
* cordova-plugin-file
* cordova-plugin-file-transfer
* cordova-plugin-ftp
* cordova-plugin-fullscreen
* cordova-plugin-media
* cordova-plugin-splashscreen
* cordova-plugin-whitelist
* cordova-plugin-zip

For locked full screen, install

* com.oddmouse.plugins.locktask

Follow his github instructions for how to create an admin reciever java class. [Instructions](https://github.com/oddmouse/cordova-plugin-locktask). Name said java reciever class "MyAdmin"

Add splash screen of your choosing to the config.xml

```xml
<platform name="android">
    <splash density="land-hdpi" src="res/load_final.png" />
    <splash density="land-ldpi" src="res/load_final.png" />
    <splash density="land-mdpi" src="res/load_final.png" />
    <splash density="land-xhdpi" src="res/load_final.png" />
    <splash density="port-hdpi" src="res/load_final.png" />
    <splash density="port-ldpi" src="res/load_final.png" />
    <splash density="port-mdpi" src="res/load_final.png" />
    <splash density="port-xhdpi" src="res/load_final.png" />
    <allow-intent href="market:*" />
</platform>
```

Cordova application is now ready to build (but has no content)

### Adding content

All pubbly related content are HTML packets, which can run locally, on a web server, or in a cordova wrapped APK. Each packed can be exported directly from the [Pubbly Design Tools](https://github.com/PubblyDevelopment/pubbly_design_tools), created and downloaded from a [Pubbly Console](https://github.com/PubblyDevelopment/pubbly_console), or manually added from the English/Swahili content root folders, found on the [GLEXP hosted repositories](https://github.com/XPRIZE/GLEXP-Team-CCI/tree/master/Cordova%20schoolHouse%20app) or TODO: downloadable from our own website. [English web root](xprize.pubbly.com/Submissions/EnglishSchoolHouseRoot.zip), [Swahili web root](xprize.pubbly.com/Submissions/SwahiliSchoolHouseRoot.zip)

### Adding content: Xprize web roots

For our English xprize application, use folder "Cordova schoolHouse app/EnglishWebRoot" hosted on the GLEXP reop. For our Swahili build, use folder "Cordova schoolHouse app/SwahiliWebRoot".

Cordova projects must be build from a computer with at least 8GB of ram.

Download either EnglishWebRoot or SwahiliWebRoot, and put it in the web root of your cordova project (schoolHouse/www)

### Adding content: Console Map packet

If you ONLY want your application to be a console map packet, you're in luck. First, create and download a map from your console server.

* Create pubbly console - [Pubbly Console](https://github.com/PubblyDevelopment/pubbly_console) section "Getting started"
* Create map nodes from Design Tools - [Pubbly Design Tools](https://github.com/PubblyDevelopment/pubbly_design_tools) section "Exports: Maps"
* Assemble map on Console - [Pubbly Console](https://github.com/PubblyDevelopment/pubbly_console) section "Assembling content: Mapping"
* Download map packet - [Pubbly Console](https://github.com/PubblyDevelopment/pubbly_console) section "Creating packets: Mapped Exports"

Create a new project and add the android platform if you haven't already

* cordova create myMap com.comp.myMap MyMap
* cd myMap
* cordova add platform android 
> Connect an android tablet for USB debugging
* cordova run android

Ensure that the cordova boiler plate project has launched on your device. If it has, extract the downloaded map packet to your cordova web root, and execute a clean build process.

* cordova clean android
* cordova build android

Check your device. It should have launched to the map you just exported from the console. Share that APK with all your friends, or sell it on the black market or something.

### Adding content: New console from scratch using our existing web structure as a base

This is a more difficult proposition.

The School House application structure was developed specifically with our Xprize program in mind. There are a few limited ways to "tweak" it to accommodate new levels, new numbers of units in each level, new subjects, new subject placements in the UI, but if you're doing anything more complicated than not-very-complicated, it might be advisable to treat all Console generated packets as "content", and write your own front end to house it.

Since I can't know for sure what modified school structure you're attempting to squeeze in, these directions will be less steps and more guidelines.

The "school/Math" subject has a Subject/Level/Unit folder structure, as does the "school/Reading/Writing" subject. Both those subjects are described in "school/school.xml", which is loaded in Javascript to create a the subject's respective pages. When a user creates a new account, a duplicate of the school.xml file is made specifically for that user. And as he finishes units in each subject, they are marked as "complete" and given a visual change.

If your school needs similarly structured level based subjects, you can make a new school.xml file to reflect the content in your file system. If you want subjects to be default "locked" or "unlocked", edit those values in the XML to fit. Any units not listed in the XML file will not be displayed in the subject specific page. The "row" and "col" values in the two subjects also effect their icon placement on screen.

Our xprize submission has three other areas of content, two of which are listed in the xml. Tutorials (which are not subject or level related) and Books (which acted as a free form bookshelf). Both tutorials and books have hardcoded icon placement. The tutorials are at the top left, in a custom expand/collapse widget. And the bookshelf is behind the icon in the top right, which launches it's own non-tracked page (books.html).

If your school wants to keep these two "floating" content areas intact, feel free to replace their school.xml entries with your own.

The final "floating" subject, added in the final update of our xprize submission, was the "Epic Quest". Epic Quest was a stand alone map packet. Unlike the Math and Reading subjects, it is not made up of Levels and Units that need to be visited sequentially, but instead interconnected map nodes, which all smartly link to each other. As such, it's representation in the school.xml is quite superficial. The regular functionality of clicking a subject is to refresh to "subject.html?NAME_OF_SUBJECT". However, the Epic Quest's click functionality was shamelessly hard coded in file js/viewSchool.js, line 382, to refresh to "school/Epic Quest/index.html". 

## Building

Once you have either added our Xprize content folders, or created a new program of your own, it's time to build your project as an APK.

It should be noted, cordova also builds to iOS, kindle, and your mothers toaster. We have not tested any of these options, however our Pubbly Engine does work on Safari on apple devices when hosted on remote servers, so it _may work just fine_, no promise.

### Building APK with English/Swahili content

Cordova was not designed with larger APKs in mind. Our original Xprize submission was under 1GB, but it quickly grew enormous. While it is possible to build APKs of +4GB size with cordova, it does take patience, luck, and a lot of waiting. 

You can make small APKs with the pubbly released tools. For instructions, see [Pubbly Console](https://github.com/PubblyDevelopment/pubbly_console) section "Creating packets: Mapped Exports".

> clean the project
* cordova clean android
> Build from powershell
* cordova build android --verbose
> It WILL fail, after about 30 minutes per gb. Build again
* cordova build android --verbose
> Keep building from powershell until the failure takes less than 5 minutes.
> Run cmd.exe as admin, cd to the project, increase java heap size (to at least twice the size of the schoolHouse/www folder)
* SET _JAVA_OPTIONS="-Xmx4000m"
> Build again. 
* cordova build android --verbose
> It will also probably fail. After it does, open task manager, kill the java process with all the ram in it. Build a final time
* cordova build android --verbose

#### FYI

It might work, but from cmd.exe as admin only. The successful build process takes +30 minutes, with a long hang on "MergeDebugAssets". Although no one in their right mind would attempt to do this on a laptop, all Pubbly submissions were indeed built on my laptop. And if, for some horrific reason, you are also attempting to build a +4GB APK with cordova on a laptop yourself... Listen to a CPU fan slowdown mid MergeDebugAssets. If that happens, the build has failed, and you can exit the command (and save about an hour of your night). Although this may just be the ghosts in my personal machine, so grain of salt.

It is also possible to get successful incremental builds by gradually increasing the size of the web root folder of cordova 0.5-1GB at a time. First build with just script files. Then add 0.5-1GB of assets and build again. Repeat until entire submission is finished. For some reason, and I honestly can't imagine why, but for some reason this usually doesn't need to error out first. However, if you add too much too quickly, you have to start all over from a fresh build (cordova clean), no amount of rebuilds will "clear it out".

Once the build succeeds, you will have an APK in your platform folder.

### Installing APK on Google Pixel C

#### Installing APK: Fresh device

First, flash your desired Android operating system. Our submission was only tested with Android 7 NMF26H

* Find desired Pixel C OS from [developers.google.com](https://developers.google.com/android/images)
* Download and unzip images
* Install ADB and FastBoot on your machine
* Flash stock Android 7 roms
> If fastboot is too old, you can manually extract and flash each image to it's partition with
    * sudo fastboot flash system system.img
> Reboot the device with
* sudo fastboot reboot
> Go through setup wizard. 
    * Setup as new device
    * Do not connect to internet
    * Set time to GMT+03:00 (Moscow)
    * Name is "CCI Xprize"
    * No unlock method
    * Turn all "Help out google" stuff off
    * All setup

#### Installing APK: Device preferences

> Cleanup homescreen
* Long drag each homescreen app to the trash
> Dismiss first time prompts
* Tap Google search bar at top of homescreen. "Close" Help build a better keyboard prompt.
* Go to 6 dots (bottom homescreen), and "Settings". From within settings...
* Screen lock -> None
> Xprize field tests posted regular analytic data to a local network FTP, so we set up regular wifi autoconnected based on their specific credentials.
* Wifi -> Add Network -> Manually fill out WE WORK Wifi Credentials

// Field
	SSID: XPRIZE
	Security: none
	Password: 
			
* Display -> Turn on Adaptive Brightness
		-> Sleep after 10 minutes
		-> When device is rotated: Stay in current orientation (landscape)
* Security -> Unknown Sources -> Allow
* Languages and Input -> Spell checker -> Off
* About tablet -> Tap build number 7 times for developer options
* Developer options -> Allow USB Debugging

#### Installing APK: ACTUALLY installing APK

* Connect Pixel C to computer
> IF computer does not FIND Pixel C, download the entire Android studio to reinstall some USB drivers.
* Swipe down from top, change android "charge this device" to "transfer files"
* Allow USB debugging
* Transfer APK from computer to device
* On device, go to Files->Pixel C
* Launch SchoolHouse.apk
* Next next, install install, after installation choose "Done" NOT "Launch"
* Move SchoolHouse icon from 6 dots to homescreen top left.

#### Installing APK: Permissions

Because the application is teaching children who don't know how to read yet, it was imperative that children would not have to read a bunch of "permissions" requests from the tablet. This was not an issue in Android 6 as permissions are set during install, but a much needed upgrade to Android 7 added additional busy work for initial setup.

* Launch SchoolHouse from homescreen
* A prompt will say "Screen is pinned...", select "No thanks"
* In app, take a User profile pic and accept "Allow access to photos, files..." prompt
* Accept "Allow Camera to access device location" prompt
* Go to book shelf, middle book, Kwa Nini Viboko... (hippo book) or another book with a Record target
* Press record button and accept the "Allow SchoolHouse to record" prompt
* Use the Square button to close the app
> All permissions have been accepted for new users.

#### Installing APK: Delete data you created to dismiss permissions.

* Go to Files->Pixel C
* Delete android_asset... (Recording from hippo book)
* Ensure Pixel C is connect to computer, and in file transfer mode, with debug enabled
* Relaunch SchoolHouse application
* Launch Chrome or Chromium from your connected computer, and start remote debugging the device
* Navigate to the "Log in" page, you should see a picture of your user account
* Open the JS console on your computer
* run...
* deleteFile("users.xml");
* With the bottom right "back" button, return to the launch page
* Return back to the login page, and double check that there are no user accounts on the device (delete worked)
> For non-debug APKs, you could also manually delete the users.xml file from an adb shell command, but we always used a debug APK.

#### Installing APK: (Optional) Force a locked Kiosk mode

To ensure the application automatically starts on launch, in a full screen un-quitable kiosk mode, 

* On computer, ensure adb is connected by issuing
	adb devices
	response -- {SerialNumber}    device
* Enter shell
	adb shell
	response -- dragon:/ $
* Set SchoolHouse as admin
	dpm set-device-owner com.cci.schoolHouse/.MyAdmin
	response -- Success: Something something, who cares, success...
* Square button on tablet, close all apps.
* Launch Pubbly from homescreen. Screen will pin.

You can remove the device owner as long as your ADB connection stays alive. As soon as you disconnect the cable, you will never be able to uninstall or even close the pubbly application. The only way to "reset" is to manually reboot to the bootloader (holding pow and vol-down keys on restart) and flash fresh images.

And if you somehow for some reason set-device-owner on a flashing locked tablet, you'd better like our submission, because your tablet won't do much else.

#### Installing APK: (Optional) DO NOT Force a locked Kiosk mode

If you do NOT want your build to be in Kiosk mode, change the file "schoolHouse/js/viewIndex.js" to reflect your preferences. If you want the application to autoStart and auto hide the bottom navigation buttons, use

```js
document.addEventListener("deviceready", function () {
    viewportFix();
    AndroidFullScreen.showSystemUI(function () {
        cordova.plugins.autoStart.enable();
        window.location.href = "welcome.html?firstLaunch";
    });
});
```

If you don't want autoStart or hidden navigation buttons, use

```js
document.addEventListener("deviceready", function () {
    viewportFix();
    window.location.href = "welcome.html?firstLaunch";
});
```

The tablet is now FULLY installed, and you can create TWRP system images

### Generating TWRP system images from installed Pixel

#### Generating images: 

* Reboot your tablet into fastboot mode
    * If adb is still connected, "adb reboot bootloader"
    * If not, manually reboot with "pow vol-down" hold
* Download [TWRP 3.0.2-23 dragon for Pixel C](https://androidfilehost.com/?fid=24727334850396245)
* Flash TWRP to recovery
* sudo fastboot flash recovery path/to/twrp.img
* sudo fastboot reboot
* Hold "pow vol-down" for bootloader
* Select "Android Recovery" (arrow down with volume buttons, confirm with power)
> Android recovery is actually TWRP recovery, cause flash
* Once TWRP has loaded, swipe right to allow modifications
* Choose "Backups"
* Check that ONLY the "Data" partition is selected
* Rename the stamp to whatever you want (I use a timestamp)
* Swipe right to back up
* Remove backup from device
    * cd ~/XprizeImage
    * adb pull /sdcard/TWRP/BACKUPS/serialno/NameOfBackup
    OR
    * Install working MTP drivers
    * Mount TWRP to local
    * Manually move backup from SD card to desired location

That folder of images is the entire Xprize submission.

## Deploying

The deploy process is equally complicated, and we wrote both Bash and Shell scripts to automate the headache. For more detailed instructions, checkout [Pubbly Submission Installation](https://github.com/PubblyDevelopment/pubbly_submission_installation)