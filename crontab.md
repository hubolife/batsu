Set up the cronjob

Now we have to make sure, that this script is run every 30 minutes. 
This is done via crontab, but we have to get your timezone first.
 In case you forgot to set it in the initial Raspberry Pi setup, you can do that now. Otherwise, you will only copy the timezone.
 Type in  tzselect and choose your location. After typing in your location details, you will get some information about your timezone.
 The most important part you need to copy is something like this TZ=’Europe/Ljubljana’ . Open up crontab by typing in crontab -e . go to the bottom and paste in your timezone. 
 The correct timezone is needed in order to calculate the times correctly later on.

If you’re planning on using DHT22 then add a newline and type in 0,30 * * * * /usr/bin/python /root/Raspberry-Weather/production/getInfo.py . 
This will tell crontab to run the script located in /root/Raspberry-Weather/getInfo.py every 30 minutes.


pi@raspberrypi:/home/batsu/Raspberry-Weather-master/production $ sudo crontab -l
# Edit this file to introduce tasks to be run by cron.
#
# Each task to run has to be defined through a single line
# indicating with different fields when the task will be run
# and what command to run for the task
#
# To define the time you can provide concrete values for
# minute (m), hour (h), day of month (dom), month (mon),
# and day of week (dow) or use '*' in these fields (for 'any').#
# Notice that tasks will be started based on the cron's system
# daemon's notion of time and timezones.
#
# Output of the crontab jobs (including errors) is sent through
# email to the user the crontab file belongs to (unless redirected).
#
# For example, you can run a backup of all your user accounts
# at 5 a.m every week with:
# 0 5 * * 1 tar -zcf /var/backups/home.tgz /home/
#
# For more information see the manual pages of crontab(5) and cron(8)
#
# m h  dom mon dow   command

# Capture Indoor temperture every hour

0 * * * * sudo  python /home/batsu/Raspberry-Weather-master/production/getInfo.py > /home/batsu/crontab.log 2>&1

# Capture Outdoor Temp. every hour

1 * * * * sudo  python /home/batsu/Raspberry-Weather-master/production/getInfoOut.py > /home/batsu/crontabOut.log 2>&1


==============================================================================
