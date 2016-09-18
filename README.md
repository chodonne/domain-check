# Domain Expiration Check Shell Script
This script checks to see if a domain has expired. It can be run in both interactive and batch mode, and provides facilities to alarm (notify via email) if a domain is about to expire before it happens. This script supports additional C/TLDs .in, .biz, .org and .info domains, and also includes a 5 second delay to avoid whois server rejecting query.

## Credits

 - Original credit to matty91 at gmail dot com - but this script has forks and modifications all over the internet
 - pulled source from https://github.com/ashworthconsulting/domain-check
 - found gist that built on above that fixed .org and other TLDs at https://gist.github.com/mrrcollins/9a668109fa8a97f9fb90

## Sample usage
Display expiration date and registrar for theos.in domain:
`domain-check -d {domain-name}`

	$ domain-check -d theos.in

Output:

	Domain                              Registrar         Status   Expires     Days Left
	------------------------------- ----------------- -------- ----------- ---------
	theos.in                            et4India (R7-AFIN Valid    28-Oct-2009   799

You can also get an email if ‘theos.in’ is going to expire in 30 days:

	$ domain-check -a -d theos.in -q -x 30 -e you@yourdomain.com

However, the most killer feature is that you can read a list of domain names from a file, such as ‘mydomains.txt’ (list each domain on a new line):

	$ domain-check -a -f mydomains.txt -q -x 30 -e you@yourdomain.com

…or…

	$ domain-check -f mydomains.txt

Output:

	Domain                              Registrar         Status   Expires     Days Left
	------------------------------- ----------------- -------- ----------- ---------
	theos.in                            et4India (R7-AFIN Valid    28-Oct-2009   799
	nixcraft.org                        oDaddy.com, Inc.  Valid    13-Aug-2009   723
	vivekgite.com                       MONIKER ONLINE SE Valid    18-aug-2010   1093
	cyberciti.biz                                         Valid    30-Jun-2009   679
	nixcraft.info                       oDaddy.com Inc. ( Valid    26-Jun-2009   675
	nixcraft.net                        GODADDY.COM, INC. Valid    11-dec-2009   843

## Default Settings

Below are the default settings in the script. These values can be overridden with any of the following files:

1. ~/.domain-check.conf

2. domain-check.conf (in same directory as the script)

3. /etc/domain-check.conf

If duplicate settings are in multiple config files, the higher level takes precedence (e.g. config in 1 will override 2).


#### Who to email when an expired domain is detected (cmdline: -e)
ADMIN="sysadmin@example.com"

#### Number of days in the warning threshhold  (cmdline: -x)
WARNDAYS=30

#### If QUIET is set to TRUE, don't print anything on the console (cmdline: -q)
QUIET="FALSE"

#### Don't send emails by default (cmdline: -a)
ALARM="FALSE"

#### Whois server to use (cmdline: -s)
WHOIS_SERVER="whois.internic.org"

#### Location of system binaries
AWK="/usr/bin/awk"

WHOIS="/usr/bin/whois"

DATE="/bin/date"

CUT="/usr/bin/cut"

MAIL="/bin/mail"

#### Place to stash temporary files
WHOIS_TMP="/var/tmp/whois.$$"


