# myalerts-phperror
Send email alert if a php error occured.

## Usage
Before using it, you have to change the settings in `/etc/myalerts/phperror.config`.

### Example configuration (assuming you have three websites running on the same server)
```sh
MYALERTS_EMAIL="user@example.com"

# you need to specify every log files here with a nickname (if your path contains space, use "quote marks")
MYALERTS_LOG_FILES=(
	root /var/log/apache2/error.log
	firstsite /var/log/apache2/firstsite-error.log
	second-site /var/log/apache2/second-site-error.log
	"third site" "/var/log/apache2/third site-error.log"
)

# you can ignore some regex patterns if you do not want to be notified of them
MYALERTS_IGNORE_PATTERNS=(
	'^\[[A-Z][a-z]{2} [A-Z][a-z]{2} [0-9]{2} [0-9]{2}:[0-9]{2}:[0-9]{2}.[0-9]{6} [0-9]{4}\] \[mpm_prefork:notice\] \[pid [0-9]+\] AH[0-9]+: Graceful restart requested, doing restart$'
	'^\[[A-Z][a-z]{2} [A-Z][a-z]{2} [0-9]{2} [0-9]{2}:[0-9]{2}:[0-9]{2}.[0-9]{6} [0-9]{4}\] \[mpm_prefork:notice\] \[pid [0-9]+\] AH[0-9]+: Apache/[^ ]+ ([^ ]+) mpm-itk/[^ ]+ OpenSSL/[^ ]+ configured -- resuming normal operations$'
	'^\[[A-Z][a-z]{2} [A-Z][a-z]{2} [0-9]{2} [0-9]{2}:[0-9]{2}:[0-9]{2}.[0-9]{6} [0-9]{4}\] \[core:notice\] \[pid [0-9]+\] AH[0-9]+: Command line: '"'"'/usr/sbin/apache2'"'"'$'
	'^\[[A-Z][a-z]{2} [A-Z][a-z]{2} [0-9]{2} [0-9]{2}:[0-9]{2}:[0-9]{2}.[0-9]{6} [0-9]{4}\] \[mpm_prefork:notice\] \[pid [0-9]+\] AH[0-9]+: caught SIGTERM, shutting down$'
)
```

It will use your server's mail system, so if you want this script to work properly you have to setup one for outgoing mails.

## Installation
- You can either [download](https://github.com/tamas646/myalerts-phperror/raw/main/myalerts-phperror_1.3.0_all.deb) and install the deb package or use the source code and setup it yourself.

- If you wish, you can install it from my apt repository too:

  ```sh
  sudo echo "deb http://apt.ptamas.hu/main/ ./" > /etc/apt/sources.list.d/apt.ptamas.list
  wget -O- https://apt.ptamas.hu/ptamas-pub.gpg |sudo apt-key add -
  apt update && apt install myalerts-phperror
  ```
