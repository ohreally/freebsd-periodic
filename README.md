# FreeBSD periodic scripts

Some additional checks and status reports for FreeBSD.

See the comments at the top of the files for instructions on how to install and enable the scripts.<br>
Following the [Filesystem Hierarchy Standard](https://refspecs.linuxfoundation.org/FHS_3.0/fhs/ch04s09.html), the scripts should be installed under `/usr/local`.

The scripts are executed in alphanumeric order of filenames. The current numbering made sense to me, but of course you should feel free to change the order for your systems.

See [periodic(8)](https://www.freebsd.org/cgi/man.cgi?query=periodic&apropos=0&sektion=0&manpath=FreeBSD+13.0-RELEASE+and+Ports&arch=default&format=html) and [periodic.conf(5)](https://www.freebsd.org/cgi/man.cgi?query=periodic.conf&sektion=5&apropos=0&manpath=FreeBSD+13.0-RELEASE+and+Ports) for more information about FreeBSD's *periodic*.

The advantage of using the *periodic* system over cron jobs for checks and status reports, is that *periodic* collects the output for all scripts in a single email (or log file), whereas running separate cron jobs for the same scripts would result in a separate mail for each script.

## `/usr/local/etc/periodic/daily/435.status-memory`

Displays the amount of memory and swap in use and free.

Keep in mind that this is just a snapshot taken at the moment the script is executed.

This script needs [sysutils/freecolor](https://www.freshports.org/sysutils/freecolor) to be installed.

## `/usr/local/etc/periodic/daily/436.status-temperature`

Displays the system temperature.

Keep in mind that this is just a snapshot taken at the moment the script is executed.

If [sysutils/smartmontools](https://www.freshports.org/sysutils/smartmontools) is installed, this script will also display the temperature for S.M.A.R.T. enabled hard disks.

## `/usr/local/etc/periodic/daily/485.status-torrelay`

If your server runs a [Tor](https://www.torproject.org/) relay, this script will display some statistics.

This script runs well for simple single-instance non-exit relays. If you have a more advanced Tor relay setup, be sure to check the `###FIXME` and `###TODO` comments in the script.

If your server does not currently run a Tor relay, please consider doing so: [Tor Project | Relay Operations](https://community.torproject.org/relay/).

*Privacy is a human right*

## `/usr/local/etc/periodic/security/105.immutable`

This script displays changes in files and directories that have [the immutable flag](https://en.wikipedia.org/wiki/File_attribute#4.4BSD_and_derivatives) set.

Since these files should not be changed, it is rather important to be alerted if they do.

## `/usr/local/etc/periodic/security/106.undeletable`

This script displays changes in files and directories that have [the undeletable (no-unlink) flag](https://en.wikipedia.org/wiki/File_attribute#4.4BSD_and_derivatives) set.

Since these files should not be deleted, it is rather important to be alerted if they do, or if their undeletable flag is changed.

## `/usr/local/etc/periodic/security/795.lastlogins`

This script lists the users that have logged in to the server in the last day, including their IP addresses.

This is simply the output of the `last` command, but limited to the entries that have not been displayed before.
