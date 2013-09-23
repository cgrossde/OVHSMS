OVHSMS
======

Send SMS on the command line using the OVH SOAP API

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