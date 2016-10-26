# AppStore Extractor Script
Script to extract Installer packages from the Apple AppStore for macOS. 

### IMPORTANT
Before you start using this script, please make sure to have the needed licenses covered (for example by site license, VPP or single licenses).

This script was tested under OS X Mavericks 10.9.5, Yosemite 10.10.5, OS X El Capitan 10.11.0 and macOS Sierra 10.12.0.

Based on an idea from Tim Sutton and Rich Trouton for downloading from the AppStore:
http://derflounder.wordpress.com/2013/10/19/downloading-microsofts-remote-desktop-installer-package-from-the-app-store/

Rich although published a detailed tutorial on how to use the script:
https://derflounder.wordpress.com/2015/11/19/downloading-installer-packages-from-the-mac-app-store-with-appstoreextract/


### How to use
This script needs the temporary download folder from the AppStore App, this is individual by host and is extracted from within the script using "getconf DARWIN_USER_CACHE_DIR".

If you want to activate the AppStore debug mode (not needed for using this script) and check the folder by hand:
__ATTENTION: This is no longer working with macOS Sierra 10.2 and higher, but is not needed for the script to work.__
  - Quit the AppStore.app if it is running
  - open the terminal and enter
    `defaults write com.apple.appstore ShowDebugMenu -bool true`
  - Start AppStore.app and browse the Menu "Debug"

If you want to check what folder is used by the AppStore.app, enter this command into your terminal:
`getconf DARWIN_USER_CACHE_DIR`

- The script generates and uses the directory "/Users/Shared/AppStore_Packages" as a destination, if you want to change this, just edit the script

- Open terminal and start this script (make it executable first), keep the window open. To make the package naming more munki friendly (using a "-" instead of "_") use the "-m" option to start the script: `AppStoreExtract.sh -m`

- Back in the AppStore.app login in to your account and navigate to your purchases (or buy a new App)
  - Click "Install" for all desired packages
  - wait till every download/installation has finished

- go back to the terminal and continue the script by pressing any key to stop processing downloads

- answer the following question with yes (y) to finalize and clean up the downloaded packages


### Known Problems
If the App ist to small (didn't find an exact size) the extraction might fail sometime, probably when the installation is finished to fast.
