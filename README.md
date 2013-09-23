OVHSMS
======

Send SMS on the command line using the OVH SOAP API

You can use `-l channel` if you have a script that checks if a service is running continously and sends you an SMS if not. With `-l channel` the script will be allowed to send one SMS only. After that you need to unlock the channel with `sms -U channel`. So every time you service is up you call `sms -U channel` and every time it is down you call `sms -l channel -m ...`, no need to worry that your script sends you 100 down notices via SMS. OVHSMS keeps internal lockfiles to keep track of open and closed channels.

Commands:

	-s 			- Sends a SMS
	-U channel	- Unlocks a channel
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
