# wcsu-scripts

There are two scripts in this repository that, together, allow arclight to automatically detect changes to EADs and re-index them.

## monitorEADsForChanges.sh
The first script is monitorEADsForChanges.sh . It does what it says on the tin--it monitors the EADs directory for changes, then saves those changes to the file arclight_fileChanges.txt . This script is most useful if it is always running. To set it to always run, even after the machine reboots, you can add it to the arclight user's crontab.

open crontab in a terminal using the text editor nano (because nano is the best command-line text editor for quick and dirty editing.)
> EDITOR=nano crontab -e

Add the line (double-check that your script is in the same place, or modify as needed)
> @reboot    sleep  90 && source ~/.bash_profile && /home/arclight/scripts/monitorEADsForChanges.sh

This will run the script monitorEADsForChanges.sh 90 seconds after the server starts up.

## stripDatesAndEvents.sh
The second script is stripDatesAndEvents.sh . It reads in a line from arclight_fileChanges.txt, indexes the changed file, copies the line to processed.txt, and deletes the line from arclight_fileChanges. Then it moves on to the next line.

This script does not need to run constantly. Currently, it's set to run once an hour on the hour on the server. You can set this up using crontab as follows:
> EDITOR=nano crontab -e

Add the line
> 0 * * * *  ~/scripts/stripDatesAndEvents.sh

Visit crontab.guru for guidance on running the script at different times using crontab.

