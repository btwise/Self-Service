Self-Service
============

CocoaDialog based self-service scripts

This script is used in tandem with CocoaDialog to present users with a GUI interface for triggering scripts to be run as root.

In its current state it provides users the ability to:
	- Change timezones
	- Sync date & time with an internal time server and fail over to Apple's if the internal is unavaiable
	- Clear the prompt that an improper shutdown occured the last time it shut down

In the GUI users pick which action(s) they want to perform and the GUI script uses the `touch` command to create the trigger file.

This is only the script piece that allows users to interact wiht the action scripts.
The actions are setup based off of Recipe 4 of http://www.macnews.com/articles/mactech/Vol.25/25.09/2509MacEnterprise-launchdforLunch/index.html

Create a directory to store the triggers so users can "touch" them
mkdir -p /Library/Management/Triggers/TimeZone
mkdir -p /Library/Management/Triggers/clearImproperShutdownWarning
sudo chown root /Library/Management/Triggers/
sudo chmod 755 /Library/Management/Triggers/
sudo chown root /Library/Management/Triggers/TimeZone
sudo chmod 777 /Library/Management/Triggers/TimeZone
sudo chown root /Library/Management/Triggers/clearImproperShutdownWarning
sudo chmod 777 /Library/Management/Triggers/clearImproperShutdownWarning

Create a LaunchDaemon using the "WatchPaths" key to watch the trigger directory.
The script determines what timezone to set the system to based on what file is present in the TimeZone directory.


