SHORT FUTURE IMPROVEMENTS
-------------------------

- Tree functions execute piped commands (grep, awk) on local system  when launched on remote slave which can cause more bandwith usage

FAR FUTURE IMPROVEMENTS
-----------------------

- MultiMaster support
	- Rethink of .osync_workdir/state/* files with PIDs, Host and Task Names to better identify multiple instances on the same fileset
	- Improve Master / Slave schema to Multimaster schema
	- State files should exist per replica for Multimaster schema

KNOWN ISSUES
------------

- RC3 is tested against Linux, FreeBSD and MacOS X. More testing needed in MSYS Windows environment.
- Cannot finish sync if one replica contains a directory and the other replica contains a file named the same way (Unix doesn't allow this)

UNDER WORK
----------

- Check for big files never get synced if max exec time
- sync test automation

RECENT CHANGES
--------------

- Added a routine that reinjects failed deletions for next run in order to prevent bringing back when deletion failed with permission issues
- Added treat dir symlink as dir parameter
- 27 May 2014: Osync 0.99 RC3
- Additionnal delete fix for *BSD and MSYS (deleted file list not created right)
- Fixed dry mode to use non dry after run treelists to create delete lists
- Added follow symlink parameter
- Minor fixes in parameter list when bandwidth parameter is used
- Added some additionnal checks for *BSD and MacOS environments
- Changed /bin/bash to /usr/bin/env bash for sanity on other systems, also check for bash presence before running
- Changed default behavior for quick sync tasks: Will try to resume failed sync tasks once
- Some code cleanup for state filenames and sync action names
- Fixed deletion propagation (again). Rsync is definitly not designed to delete a list of files / folders. Rsync replaced by rm function which downloads deletion list to remote system.
- Added path detection for exclude list file
- Added a simple init script and an install script
- Fixed an issue with MacOSX using rsync -E differently than other *nix (Thanks to Pierre Clement)
- Multislave asynchronous task support (Thanks to Ulrich Norbisrath)
	- This breaks compat with elder osync runs. Add the SYNC_ID suffix to elder state files to keep deleted file information.
- Added an easier debug setting i.e DEBUG=yes ./osync.sh (Again, thanks to Ulrich Norbisrath)
- Added hardlink preservation (Thanks to Ulrich Norbisrath)
- Added external exclusion file support (Thanks to Pierre Clement)
- Fixed some typos in doc and program itself (Thanks to Pierre Clement)
- More detailled verbose status messages
- More detailled status messages
- Fixed a bug preventing propagation of empty directory deletions
- Fixed a nasty bug preventing writing lock files on remote system as superuser
- Gzipped logs are now deleted once sent
- Fixed some typos (thanks to Pavel Kiryukhin)
- Fixed a bug with double trailing slashes in certain sceanrios
- Sync execution don't fails anymore if files vanish during execution, also vanished files get logged
- Add eventual "comm -23" replacement by "grep -F -x -v -f" to enhance compatibility with other platforms (comm is still much faster than grep, so we keep it)
- Replaced xargs rm with find -exec rm to better handle file names in soft deletion
- Fixed soft deletion not happening with relative paths
- Improved process termination behavior
- More code merging and cleanup
- Fixed a bug preventing deleted files in subdirectories propagation (Thanks to Richard Faasen for pointing that out)
- Some more function merge in sync process
- Dry mode won't create or modifiy state files anymore and will use dry-state files instead
- Improved file monitor mode
- Added possibility to daemonize osync in monitor mode
- Added monitor mode, which will launch a sync task upon file operations on master replica
- Changed conf file default format for ssh uri (old format is still compatible)
- Added ssh uri support for slave replicas
- Improved execution hooks logs
- Various bugfixes introduced with function merge
- Added basic MacOS X support (yet not fully tested)
- Merged tree list functions into one
- Added possibility to quick sync two local directories without any prior configuration
- Added time control on OS detection
- 02 Nov. 2013: Osync 0.99 RC2
- Minor improvement on operating system detection
- Improved RunLocalCommand execution hook
- Minor improvements on permission checks
- Made more portability improvements (mostly for FreeBSD, must be run with bash shell)
- Added local and remote operating system detection
	- Added forced usage of MSYS find on remote MSYS hosts
	- Updated MSYS handling
- Merged MSYS (MinGW minimal system) bash compatibility under Windows from Obackup
	- Added check for /var/log directory
	- Added check for shared memory directory
	- Added alternative way to kill child processes for other OSes and especially for MSYS (which is a very odd way)
	- Added Sendemail.exe support for windows Alerting
	- Replaced which commend by type -p, as it is more portable
	- Added support for ping.exe from windows
	- Forced usage of MSYS find instead of Windows' find.exe on master
       - Added an optionnal remote rsync executable path parameter
- Fixed an issue with CheckConnectivity3rdPartyHosts
- Added an option to stop execution if a local / remote command fails
- Improved forced quit command by killing all child processes
- Before / after commands are now ignored on dryruns
- Improved verbose output
- Fixed various typos
- Enforced CheckConnectivityRemoteHost and CheckConnectivity3rdPartyHosts checks (if one of these fails, osync is stopped)
- 18 Aug. 2013: Osync 0.99 RC1
- Added possibility to change default logfile
- Fixed a possible error upon master replica lock check
- Fixed exclude directorires with spaces in names generate errros on master replica tree functions
- Dryruns won't create after run tree lists and therefore not prevent building real run delete lists
- Softdelete and conflict backup functions are now time controlled
- Added bandwidth limit
- Update and delete functions now run rsync with --stats parameter
- Fixed LoadConfigFile function will not warn on wrong config file
- Added --no-maxtime parameter for sync big changes without enforcing execution time checks
- 03 Aug. 2013: beta 3 milestone
- Softdelete functions do now honor --dry switch
- Simplified sync delete functions
- Enhanced compatibility with different charsets in filenames
- Added CentOS 5 compatibility (comm v5.97 without --nocheck-order function replaced by sort)
- Tree functions now honor supplementary rsync arguments
- Tree functions now honor exclusion lists
- 01 Aug. 2013: beta 2 milestone
- Fixed an issue with spaces in directory trees
- Fixed an issue with recursive directory trees
- Revamped a bit code to add bash 3.2 compatibility
- 24 Jul. 2013: beta milestone
- Fixed some bad error handling in CheckMasterSlaveDirs and LockDirectories
- Added support for spaces in sync dirs and exclude lists
- Fixed false exit code if no remote slave lock present
- Added minimum disk space checks
- Added osync support in ssh_filter.sh
- Added support for sudo exec on remote slave
- Added support for alternative rsync executable
- Added support for spaces in sync directories names
- Added support for ACL and xattr
- Added --force-unlock parameter to bypass any existing locks on replicas
- Added full remote support for slave replica
- Improved error detection
- Made some changes in execution hook output
- Fixed an issue with task execution handling exit codes
- Added master and slave replicas lock functionnality
- Added rsync exclude patterns support
- Improved backup items, can now have multiple backups of the same file
- Added maximum number of resume tries before trying a fresh stateless execution
- Added possibility to resume a sync after an error
- Improved task execution time handling
- Improved SendAlert handling
- Fixed cleanup launched even if DEBUG=yes
- Added verbose rsync output
- Added --dry and --silent parameters
- Added time control
- Added master/slave conflict prevalance option
- Added soft-deleted items
- Added backup items in case of conflict

19 Jun. 2013: Project begin as Obackup fork

