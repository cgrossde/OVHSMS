OVHSMS
======

Send SMS on the command line using the OVH SOAP API

You can use `-l channel` if you have a script that checks if a service is running continously and sends you an SMS if not. With `-l channel` the script will be allowed to send one SMS only. After that you need to unlock the channel with `sms -U channel`. So every time you service is up you call `sms -U channel` and every time it is down you call `sms -l channel -m ...`, no need to worry that your script sends you 100 down notices via SMS. OVHSMS uses internal lockfiles to keep track of open and closed channels.

Commands:

	-s 			- Sends a SMS
	-U channel	- Unlocks a channel, use -m to send SMS if successful
	-h 			- This Help

Options:

	-m message		- The message of the SMS

	-t to			- Send to number (international format)
	-f from			- Sender number
	-a account		- SMS Account
	-u user			- SMS User
	-p password		- SMS User Password
	-l channel		- Lock given channel for given number to prevent
				  further notices
	-d email		- Debug, send Email instead

Configuration:

Configfile should be under /etc/ovhsms.conf. It uses the INI-Format:

	[Credentials]
	account=sms-gcxxxx-x
	user=XXXXX
	password=XXXXX

	[SMS]
	to=+49000000
	from=+49000000

Examples
========
Send SMS:
	
	sms -s -m "Hey, your server is down"
	sms -s -m "Another SMS to a non default number" -t "+490022334455"
	
Channels:

	sms -s -l http -m "HTTP DOWN" 
	sms -U http -m "HTTP UP"
	
	Pesudocode (eg. run by cron every 5min):
	if ( webserver down ) {
		sms -s -l http -m "HTTP DOWN"
	} else {
		sms -U http -m "HTTP UP"
	}
	
This will send one SMS when your service is down (even if you call `sms -s -l http -m "HTTP DOWN"` multiple times). And one SMS when your service back UP again.

Send email instead of SMS for testing purpose:

	sms -s -m "Hey, your server is down" -d youremail@domain.com
	sms -s -l http -m "HTTP DOWN" -d youremail@domain.com
	sms -U http -m "HTTP UP" -d youremail@domain.com
	
